
Working with XNAT using PyXNAT
==============================

Download PyXNAT Module
~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    !pip install pyxnat

Connect to server: Enter user : password
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: ipython2

    import pyxnat
    import os
    
    # connect to XNAT instance
    from pyxnat import Interface
    xnat = Interface(server='http://sharp.bidmc.harvard.edu:8080',  cachedir='/tmp')
    xnat.select.projects().get()

Different types of datatypes supported by XNAT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    xnat.inspect.datatypes()

Check number of Subject
~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    subjects = xnat.select('/projects/FAST/subjects')
    subjects.get().__len__()

Loading the project
~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    project = xnat.select.project('FAST')
    print(project)

Working with Subject Data
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    contraints = [('xnat:subjectData/SUBJECT_ID','LIKE','%'),
                      'AND', ('xnat:subjectData/PROJECT', '=', 'FAST') 
                  ]
    table = xnat.select('xnat:subjectData', ['xnat:subjectData/SUBJECT_LABEL','xnat:subjectData/PROJECT','xnat:subjectData/SUBJECT_ID']).where(contraints)
    table.__len__()

.. code:: ipython2

    print(table)

Working with MRI Session Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    contraints = [('xnat:mrSessionData/ID','LIKE','%'),
                      'AND', ('xnat:subjectData/PROJECT', '=', 'FAST')
                 ]
    table1 = xnat.select('xnat:mrSessionData', ['xnat:mrSessionData/SUBJECT_LABEL','xnat:mrSessionData/SESSION_ID']).where(contraints)
    table1.__len__()

.. code:: ipython2

    print(table1)

Filtering using Behavioral scores
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    contraints = [('xnat:subjectData/SUBJECT_ID','LIKE','%'),
                      ('behavioral:scores/VocabScore', '>=', '36'),
                      'AND', ('xnat:subjectData/PROJECT', '=', 'FAST')
                 ]
    table1 = xnat.select('xnat:subjectData').where(contraints)
    table1.__len__()

Downloading the selective data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lets start with download data for one subject

.. code:: ipython2

    subject = xnat.select.project('FAST').subject('0001')
    experiment = subject.experiment("SHARP_E00746")
    allscans = experiment.scans()
    allscans.download("/tmp", type='ALL', extract=False)

Now lets write a filer to download the selective data for all the
subjects

.. code:: ipython2

    # Filer can be developed based on the data parameters
    contraints = [('xnat:mrSessionData/ID','LIKE','%'),
                      'AND', ('xnat:subjectData/PROJECT', '=', 'FAST')
    
    list_subjects = xnat.select.project('FAST').subjects().where(contraints)
    for list_subject in list_subjects:
        list_experiments = list_subject.experiments().where(contraints)
        for list_experiment in list_experiments:
            print list_experiment
            scans = list_experiment.scans()
            try:
                # Number 2 is for Anatomical data. Similar types can be set for other data types
                scans.download("/tmp", type='2', extract=False)
            except:
                print "There are no scans to download"
