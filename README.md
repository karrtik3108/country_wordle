# Streamlit Worldle

## What's this?

- `README.md`: This Document! To help you find your way around
- `streamlit_app.py`: The main app that gets run by [`streamlit`](https://docs.streamlit.io/)
- `requirements.txt`: Pins the version of packages needed
- `LICENSE`: Follows Streamlit's use of Apache 2.0 Open Source License
- `.gitignore`: Tells git to avoid comitting / scanning certain local-specific files
- `.streamlit/config.toml`: Customizes the behaviour of streamlit without specifying command line arguments (`streamlit config show`)

### Streamlit Worldle

A geography guessing game with the following rules:

- You are given the outline of a mystery Country or Territory 🌏
- If you guess the correct Country then you win 🥳
- If you guess incorrectly 6 times then you lose 😔
- Each incorrect guess will reveal information that might help you locate the mystery Country:
    - 📏 The `distance` that the center of the guess Country is away from the mystery Country
    - 🧭 The `direction` that points from the guess Country to the mystery Country (on a 2D map)
    - 🥈 The `proximity` percentage of how correct the guess was. A guess on the opposite side of the globe will be `0%` and the correct guess will be `100%`.

### Data Sources and Caveats

- World Bank: [World Boundaries GeoDatabase](https://datacatalog.worldbank.org/search/dataset/0038272/World-Bank-Official-Boundaries)
    - Provides Country and Territory shapes, locations, and names
    - Loaded into SQLite + Spatialite database (see original location guessing [repository on github](https://github.com/gerardrbentley/streamlit-location-guesser))
    - Some boundaries may not be precise or might include satellite territories in addition to mainland
- 📏 `distance` is the [Haversine Distance](https://en.wikipedia.org/wiki/Haversine_formula) calculated based on the [centroids](http://wiki.gis.com/wiki/index.php/Centroid) of the Countries calculated using GeoPandas
    - Countries that share a border will **NOT** have 0 km `distance`
    - The maximum `distance` possible is roughly `20000 km` (two points on opposite sides of the globe)
    - The `proximity` percentage is based on the maximum `distance`
![Screenshot (36)](https://user-images.githubusercontent.com/93999235/208177092-4bfddd5f-9586-4b26-aea2-1f8ea4c161a4.png)

