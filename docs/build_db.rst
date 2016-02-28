===================
build_db
===================

An auxiliary program, build_db.py is located in sastbx_path/source/sastbx/zernike folder. As the name suggests, the script is used to build your own database (the default database used in the software is compiled using this script based on 10,733 models chosen from PISA). As most scripts in this folder, run the program without any parameter will give the usage of it. Type ``sastbx.python build_db.py`` in the command line, then:

::


  Usage: libtbx.python build_db.py path=path nmax=nmax fix_dx=True/False

  Attention: 
  The path should be a directory that contains ONLY PDB files



  db {
    path = None
      .help = "path of pdb files"
    nmax = 20
      .help = "maximum order of zernike expansion"
    fix_dx = True
      .help = "Whether keeping default dx=0.7A or not"
    np = 50
      .help = "number of point covering [0,1]"
    nprocess = 4
      .help = "number of processes"
    prefix = "myDB"
      .help = "the prefix of pickle file names"
  }

For example, if there is a directory named models_pdb which contains 3D models in pdb format, and now I want to generate a database for these models. If I want the data to be stored in the database directory ( suppose that both the directories are in home directory) and the prefixnamed "mydb", then I will write a command like this:

``sastbx.python build_db.py path=~/models_pdb prefix=~/database/mydb``

I'm just used to sastbx.python instead of libtbx.python.

Once the database created, you can search with the new database:
``sastbx.shapeup target=myquery.dat rmax=estimated_rmax dbpath=path_of_database``

Four files will be created inside the database directory: mydb.codes, mydb.nlm, mydb.nn, mydb.rmax. The .codes file records the names of the pdb files used in the database generation. .nlm file and .nn file store the 3D zernike moments and the nn coefficients for each model. .rmax file tells about each model's radius, that is, the max distance from the center to a point on the object. Data stored in these files are all in list format, and information for a specific model can be accessed with the same index.

It is also easy to read the contents stored in these files with simple python codes (run sastbx.python and run the codes interactively):

::

  from libtbx import easy_pickle
  prefix="~/database/mydb"
  codes=easy_pickle.load(prefix+".codes")
  nlm_coefs=easy_pickle.load(prefix+".nlm")
  nn_coefs=easy_pickle.load(prefix+".nn")
  rmaxs=easy_pickle.load(prefix+".rmax")
  rmaxs=easy_pickle.load("~/database")
  #retrieval information for a specific model
  code="model_of_interest" #suppose the name of the model is "model_of_interest"
  indx=codes.index(code)
  nlm_coef=nlm_coefs[indx]
  nn_coef=nn_coefs[indx]
  rmax=rmaxs[indx]
