## Estimating Global Rural Population

This project estimates the global rural population by combining data from the World Bank and WorldPop. The methodology involves data acquisition, preparation, and processing to estimate rural populations for each country.

### Data Acquisition

- **World Bank Data**: 
  - Source: [World Bank API](https://api.worldbank.org/v2/en/indicator/SP.RUR.TOTL.ZS?downloadformat=csv)
  - Content: Rural population as a percentage of the total population.

- **WorldPop Data**: 
  - Source: [WorldPop](https://www.worldpop.org/)
  - Content: High-resolution population density data.

### Data Preparation

1. Download and unzip World Bank rural population data.
2. The World Bank data is unzipped and read into a DataFrame.
3. A mean of the last 5 years (2015-2019) of rural population percentage data is calculated. If data is missing, a mean of the last 10 years (2010-2019) is used instead.
4. Clean and filter DataFrame to include `Country.Name`, `ISO_A3`, `Indicator.Name`, `rural_pop_pct_mean`.
5. Ensure dataset contains complete cases with positive rural population percentage.

### Population Density Processing

1. Load WorldPop population density raster data.
2. For each country (by ISO code):
   - Crop and mask WorldPop raster to country boundaries.
   - Crop and masks the WorldPop raster data to the country's boundaries.
   - Calculate the total population estimate by summing up the values in the raster.
   - A frequency table for each population density class is created to determine the threshold population density that defines rural areas.
   - The rural population is estimated by masking out areas with population density higher than the threshold.

### Output Generation

- Raster files for estimated rural population at 1km resolution for each country.
- Files saved with LZW compression in specified directory.

### Dependencies

- R packages for spatial data (`raster`, `sf`, `sp`).
- R packages for data downloading and processing (`httr`, `dplyr`).

### Assumptions and Limitations

- Rural areas defined based on population density thresholds.
- Estimates rely on WorldPop and World Bank data accuracy and resolution.
- Assumes spatial uniformity within raster cells.

### Potential Improvements

- Integrate additional or more recent data sources.
- Refine rural area definition using country-specific criteria.
