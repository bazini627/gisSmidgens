# <center>Smidgens of GIS</center>
## <center>Repo for bits and pieces of helpful GIS commands that I'm bound to forget and then spend forever Goggling for</center>

### Traverse directory structure  with `wget` to only download certain files
`wget -r -A zip -nd --no-parent -P data/ https://rmgsc.cr.usgs.gov/outgoing/GeoMAC/current_year_fire_data/California/Bald/`  

`-r` : Move recursively through the directory structure  
`-A zip` : will only grab file types specified; in this case only zip files  
`-nd` : don't duplicate the same dir structure we are moving through  
`--no-parent` : don't go through any of the parent directories  
`-P data/` : directory to save to and will create if doesn't exist

### Use `curl` to download data files that are all within the same directory

`curl -Lk --remote-name-all https://developer.trimet.org/gis/data/{tm_boundary,tm_parkride,tm_rail_lines,tm_rail_stops,tm_routes,tm_stops,tm_route_stops,tm_tran_cen}.zip`  

`-L` : Allows for a redirect to a different URL other than the one supplied  
`-k` : Allows for connection to a server connection that may be deemed insecure  
`--remote-name-all` : Output filenames as each individual one in the curly braces  

### Use `mapshaper` to reproject a shape file, only retain certain fields and field with specific value, simplify the lines, specify a precision for coordinates, and output to GeoJSON 
`mapshaper BND_DCD_City_Limits.shp -proj EPSG:4326 -filter-fields NAME -filter NAME=='Richmond' -simplify dp 30% -o precision=.0001 format=geojson ../data/richmondCityLimits.json`  

`-proj EPSG:4326` : reproject to WGS84  
`-filter-fields NAME` : only retain the name field from the shapefile  
`-filter NAME=='Richmond'` only keep the `NAME` fields that have a value of `Richmond`  
`-simplify dp 30%` : simplify the lines by reducing the resolution to 30%  
`-o` : output  
`precision=.001` : only keep three decimal places for the coordinates  
`format=geojson` : output to GeoJSON  
`../data/richmondCityLimits.json` : path/name to output to  


