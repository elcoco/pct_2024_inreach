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

    NOTE: The files may not show up as exactly 100 miles. This is probably due to the simplifying.
    Since the cutting was done before the simplifying, each file is in reality very close to 100 miles.

    NOTE2: I was not able to test everything so please let me know if something doesn't work as expected.
