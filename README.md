# 2024 PCT gpx files compatible with the Garmin inreach mini 2

    The great people from the PCTA made new gpx files available for us to use.

    Unfortunately the garmin inreach mini 2 can only handle 10000 points per gpx file.
    To make this data usable for inreach users I cut the large PCTA data file into separate files
    of 100 miles each.
    Each file was then simplified to contain only 10000 points.

    To create these files I used the original 2024 (march) dataset from the PCTA.
    link: https://www.pcta.org/discover-the-trail/maps/pct-data/

    Tools i used for cutting and simplifying:
    - gpsbabel:  https://www.gpsbabel.org
    - gpxslicer: https://pypi.org/project/gpxslicer
    - viking:    https://github.com/viking-gps/viking
    - qmapshack: https://github.com/Maproom/qmapshack

    NOTE: The files may not show up as exactly 100 miles. This is probably due to the simplifying.
    Since the cutting was done before the simplifying, each file is in reality very close to 100 miles.

    NOTE2: I was not able to test everything so please let me know if something doesn't work as expected.

## Download

    If you are a git user, you know what to do.
    If not, you can download this project and GPX files by clicking the "code" button and then press "Download Zip"

## Process
    
    # Use qmapshack to put tracks in right order and export as gpx

    # convert gpx to csv and remove duplicate data
    gpsbabel -i gpx -f source.gpx -o csv -F tmp.csv
    cat tmp.csv | uniq > dest.csv

    # convert csv to single track gpx file
    gpsbabel -i csv -f source.csv -x transform,trk=wpt -x nuketypes,waypoints -o gpx -F dest.gpx

    # split gpx into 100 mile tracks
    # source: https://pypi.org/project/gpxslicer/
    gpxslicer -i source.gpx -d 160934 > dest.gpx

    # use viking gpx editor to save every track to file

    # remove conflicting extensions tag in gpx file
    sed -i '7d' pcta_0000.gpx
    sed -i '7d' pcta_0100.gpx
    ...

    # convert every gpx file to 10000 points max
    mkdir ./inreach
    for f in *.gpx ; do gpsbabel -i gpx -f "$f" -x simplify,count=10000 -o gpx -F "inreach/$f" ; done
