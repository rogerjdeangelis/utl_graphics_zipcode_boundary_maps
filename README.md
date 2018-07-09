# utl_graphics_zipcode_boundary_maps
US zipcode boundary maps.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.


    US zipcode boundary maps

    see for graphic output
    https://tinyurl.com/y9orffpw
    https://github.com/rogerjdeangelis/utl_graphics_zipcode_boundary_maps/blob/master/utl_graphics_zipcode_boundary_maps.pdf


    github
    https://github.com/rogerjdeangelis/utl_graphics_zipcode_boundary_maps

    I had to upgrade ggplot2 to the latest version

    see StackOverflow R
    https://tinyurl.com/yafd6dpy
    https://stackoverflow.com/questions/51211239/how-to-create-zipcode-boundaries-in-r

    Camille profile
    https://stackoverflow.com/users/5325862/camille


    * has SAS examples of graphics and a  zipcode boundary;

    https://tinyurl.com/yceo4rfj
    https://github.com/rogerjdeangelis/utl_graphics_589_SAS_and_R_graphics_with_code_and_datasets

    for other graphics
    https://tinyurl.com/ybum4kry
    https://github.com/rogerjdeangelis?utf8=%E2%9C%93&tab=repositories&q=graphics&type=&language=


    INPUT
    =====

     WORK.WANT total obs=10

       AREA             ZIP

       Tooele          84074
       Tooele          84029
       NEUtahCo        84003
       NEUtahCo        84004
       NEUtahCo        84042
       NEUtahCo        84062
       NWUtahCounty    84005
       NWUtahCounty    84013
       NWUtahCounty    84043
       NWUtahCounty    84045


     EXAMPLE OUTPUT
     --------------
     https://tinyurl.com/y9orffpw


    PROCESS (WPS/PROC R - Working Code)
    ====================================

      utah_zips<-read_sas("d:/sd1/have.sas7bdat");
      zips_sf <- zctas(cb = T, starts_with = "84", class = "sf") %>%
        select(zip = ZCTA5CE10, geometry);
      head(zips_sf);
      utah_sf <- zips_sf %>%
        inner_join(utah_zips, by = "zip");
      head(utah_sf);
      basemap <- get_map(location = c(lon=-111.9, lat= 40.7), zoom = 9);
      zmap<-ggmap(basemap) +
        geom_sf(aes(fill = zip), data = utah_sf, inherit.aes = F, size = 0, alpha = 0.6) +
        coord_sf(ndiscr = F) +
        theme(legend.position = "none");

    OUTPUT
    ======

     https://tinyurl.com/y9orffpw

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;
    options validvarname=v7;
    * lowercase names works better;
    libname sd1 "d:/sd1";
    data sd1.have;
    informat area $13.;
    input area zip$;
    cards4;
    Tooele 84074
    Tooele 84029
    NEUtahCo 84003
    NEUtahCo 84004
    NEUtahCo 84042
    NEUtahCo 84062
    NWUtahCounty 84005
    NWUtahCounty 84013
    NWUtahCounty 84043
    NWUtahCounty 84045
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    * WORKS;
    %utlfkil(d:/pdf/utl_graphics_zipcode_boundary_maps.pdf); *delete;

    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk "%sysfunc(pathname(work))";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    options(tigris_use_cache = TRUE);
    library(haven);
    library(tidyverse);
    library(tigris);
    library(ggmap);
    library(ggplot2);
    utah_zips<-read_sas("d:/sd1/have.sas7bdat");
    zips_sf <- zctas(cb = T, starts_with = "84", class = "sf") %>%
      select(zip = ZCTA5CE10, geometry);
    utah_sf <- zips_sf %>%
      inner_join(utah_zips, by = "zip");
    basemap <- get_map(location = c(lon=-111.9, lat= 40.7), zoom = 9);
    zmap<-ggmap(basemap) +
      geom_sf(aes(fill = zip), data = utah_sf, inherit.aes = F, size = 0, alpha = 0.6) +
      coord_sf(ndiscr = F) +
      theme(legend.position = "none");
    ggsave(zmap, file = "d:/pdf/utl_graphics_zipcode_boundary_maps.pdf");
    endsubmit;
    run;quit;
    ');


    * LOG;

    > utah_zips<-read_sas("d:/sd1/have.sas7bdat")
    > zips_sf <- zctas(cb = T, starts_with = "84", class = "sf") %>%  select(zip = ZCTA5CE10, geometry)
    > utah_sf <- zips_sf %>%  inner_join(utah_zips, by = "zip")
    > basemap <- get_map(location = c(lon=-111.9, lat= 40.7), zoom = 9)
    Map from URL : http://maps.googleapis.com/maps/api/staticmap?center=40.7,-111.9
    &zoom=9&size=640x640&scale=2&maptype=terrain&language=en-EN&sensor=false
    > zmap<-ggmap(basemap) +  geom_sf(aes(fill = zip), data = utah_sf,
    inherit.aes = F, size = 0, alpha = 0.6) +  coord_sf(ndiscr = F) +  theme(legend.position = "none")
    Coordinate system already present. Adding new coordinate system, which will replace the existing one.
    > ggsave(zmap, file = "d:/pdf/utl_graphics_zipcode_boundary_maps.pdf")

    Saving 7 x 7 in image


