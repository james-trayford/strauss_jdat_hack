# JDAViz - STRAUSS Hack day!

You can clone this repository locally:

`git clone git@github.com:james-trayford/strauss_jdat_hack.git /path/to/your/directory`

and then initialise any submodules:

`cd /path/to/your/directory`
`git submodule update --init --recursive`

### Python and setting up an environment:

This should work with python versions `3.8` to `3.11`.

We can set up an environment for this hacke inside the repository, using:

`python3 -m venv venv`
`source venv/bin/activate`

and install all the relevant modules using:

`pip install -r requirements_slim.txt`

This may take a while first time. After that, you may want to override things like `jdaviz` with local copies, say if we want to edit the library on the fly. 

### Notebooks

We have a few notebooks as a starting point in the `./notebook/` directory. This includes:

1. An introduction to _"Spectral Audification"_ technique in `./notebook/SpectralData.ipynb`
2. An introduction to seamless audio in python and some of the associated issues in `./notebook/AudioIntro.ipynb`
3. A version of [This JDAT notebook with appended sound functionality](https://github.com/spacetelescope/jdat_notebooks/blob/main/notebooks/IFU_cube_continuum_fit/NGC4151_FeII_ContinuumFit.ipynb) in `./notebook/NGC4151_FeII_ContinuumFit.ipynb`

### Listener App

To see our prototype listener application, using Python `Flask` and JS to allow us to demonstrate this technique. This is set-up as a submodule on a custom branch for these sessions. The example we listen to here will be the same as the cube in `./notebook/NGC4151_FeII_ContinuumFit.ipynb`.

To initialise this (having run the `submodule` command above), you can run a couple of initial python programs, first change into the directory

`cd /hyperspectral_listener/listener-app/`

get the data we want:

`python3 get_data.py`

ands initialise the cube:

`python3 render_soundgrid.py`

Once this is done, we can serve the application using something like:

`gunicorn -b localhost:8000 --timeout 500 app:app --log-level debug`

Which should make the application available at browser address:

`localhost:8000`

When running for the first time go to _"Select New"_ and open the data cube at `/path/to/your/directory/hyperspectral_listener/listener-app/DataCubes/NGC4151_Hband.fits`


### .Astronomy 13 hack

There are some rough materials from the _.Astronomy 13_ hack day that could be usful here... its in `./dotAstro13_hack/`.

Here we use canvases to render sonifications of paths from MaNGA property maps. This can be done in a call-response style (as opposed to real-time, you can draw a path, thne render, then listen)

You will also neeed to download the big data cube for this, e.g.

`cd ./dotAstro13_hack/manga`
`curl -O 'https://data.sdss.org/sas/dr17/manga/spectro/redux/v3_1_1/7443/stack/manga-7443-12703-LOGCUBE.fits.gz'`
`cd ../..`