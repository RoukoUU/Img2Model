## Facial Capture
This is a Python package to fit 3D morphable models (3DMMs) to images of
faces. It mainly provides classes to work with and render 3DMMs, and
functions that use these classes to optimize the objective of fitting
3DMMs to a source RGB image or a video for facial performance capture.

![Facial Capture Example](data/facial_capture.gif)

## Features
-   Fit a 3DMM shape model to a RGB image
-   Joint optimization of rendering pixel error and landmarks fitting
-   Fit a 3DMM texture model with spherical harmonic lighting to a
    source RGB image
-   Recover the barycentric parameters of the underlying verticles from
    the 3DMM mesh triangles that contribute to each pixel of a person's
    face in an image
-   Extract per vertex texture
-   Track expressions and spherical harmonic lighting over a sequence of
    images (or a video)

## Prerequisites
-   Python 3
-   Install all requirements with `pip`:
    `pip install -r requirements.txt .`
-   Install face2face library:
    `pip install -e .`
-   If you run into issues with creating wheels for OpenGL, clone this repository -> https://github.com/mcfletch/pyopengl.git
    then install and run the following commands in this order in your Img2Model directory:
    `cd pyopengl`
    `pip install -e .`
    `cd accelerate`
    `pip install -e .`

You need to download 2017 BFM model as we aren't allowed to share it:

-   Create models folder under Facial-Capture
-   Download Basel model 2017 model from
    [here](<https://faces.dmi.unibas.ch/bfm/bfm2017.html>) to models
    folder
-   Process via `python processBFM2017.py`

Also you would need the trained landmark dlib predictor:

-   Download and extract shape\_predictor\_68\_face\_landmarks from
    [here](<http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2>)
    to models folder

## Running
-   First create a face identity (use 1 to 3 images max) using

    ```python
    python cli/initialize.py --input_dir path_to_init_images --output_dir path_to_save_identity
    ```

-   (If an error occurs where CV2 is not present, install CV2 with `pip install opencv-python`)

-   After creating the identity, you can now track the expressions
    using:

    ```python
    python cli/tracker.py --input_dir path_to_tracking_images --output_dir path_to_save_tracking --parameters path_to_save_identity/params.npy
    ```

-   I have included 1 example of a succesful operation - the sample can be found in identity_raw and the results in identity_f2f. This was achieved by running

    ```python
    python.exe .\cli\initialize.py --input_dir "..\identity_raw" --output_dir "..\identity_f2f"
    ```
