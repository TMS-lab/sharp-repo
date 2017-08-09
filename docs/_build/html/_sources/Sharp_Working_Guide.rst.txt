
Working with XNAT using PyXNAT
==============================

Download PyXNAT Module
~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    !pip install pyxnat


.. parsed-literal::

    Collecting pyxnat
      Downloading pyxnat-1.0.0.0.tar.gz (540kB)
    [K    100% |████████████████████████████████| 542kB 1.6MB/s ta 0:00:011
    [?25hRequirement already satisfied: requests in /Library/Python/2.7/site-packages (from pyxnat)
    Requirement already satisfied: lxml in /Library/Python/2.7/site-packages (from pyxnat)
    Requirement already satisfied: idna<2.6,>=2.5 in /Library/Python/2.7/site-packages (from requests->pyxnat)
    Requirement already satisfied: certifi>=2017.4.17 in /Library/Python/2.7/site-packages (from requests->pyxnat)
    Requirement already satisfied: urllib3<1.23,>=1.21.1 in /Library/Python/2.7/site-packages (from requests->pyxnat)
    Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /Library/Python/2.7/site-packages (from requests->pyxnat)
    Building wheels for collected packages: pyxnat
      Running setup.py bdist_wheel for pyxnat ... [?25ldone
    [?25h  Stored in directory: /Users/raminder/Library/Caches/pip/wheels/2d/79/f1/4a31fb18b992650bbd099574ce9675286db813ad3556282ccc
    Successfully built pyxnat
    Installing collected packages: pyxnat
    Successfully installed pyxnat-1.0.0.0


Connect to server: Enter user : password
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: ipython2

    import pyxnat
    import os
    
    # connect to XNAT instance
    from pyxnat import Interface
    xnat = Interface(server='http://sharp.bidmc.harvard.edu:8080',  cachedir='/tmp')
    xnat.select.projects().get()


.. parsed-literal::

    User: admin
    ········




.. parsed-literal::

    ['SHARP_1A', 'FAST', 'INSIGHT', 'SHARP_2B']



Different types of datatypes supported by XNAT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    xnat.inspect.datatypes()




.. parsed-literal::

    ['xnat:qcAssessmentData',
     'xnat:investigatorData',
     'xnat:qcManualAssessorData',
     'xnat:petmrSessionData',
     'xnat:subjectData',
     'xnat:crSessionData',
     'val:protocolData',
     'xnat:subjectVariablesData',
     'xnat:petSessionData',
     'xnat:pVisitData',
     'xnat:mrSessionData',
     'xnat:ctSessionData',
     'xnat:projectData',
     'xnat:eegScanData',
     'behavioral:scores',
     'xnat:eegSessionData']



Check number of Subject
~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    subjects = xnat.select('/projects/FAST/subjects')
    subjects.get().__len__()




.. parsed-literal::

    92



Loading the project
~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    project = xnat.select.project('FAST')
    print(project)


.. parsed-literal::

    <Project Object> FAST


Working with Subject Data
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    contraints = [('xnat:subjectData/SUBJECT_ID','LIKE','%'),
                      'AND', ('xnat:subjectData/PROJECT', '=', 'FAST') 
                  ]
    table = xnat.select('xnat:subjectData', ['xnat:subjectData/PROJECT','xnat:subjectData/SUBJECT_ID','xnat:subjectData/SUBJECT_LABEL']).where(contraints)
    table.__len__()




.. parsed-literal::

    92



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




.. parsed-literal::

    159



.. code:: ipython2

    print(table1)


.. parsed-literal::

    subject_label,session_id
    0001,SHARP_E00746
    0001,SHARP_E00747
    0002,SHARP_E00467
    0002,SHARP_E00463
    0003,SHARP_E00664
    0003,SHARP_E00663
    0004,SHARP_E00008
    0004,SHARP_E00001
    0005,SHARP_E00752
    0005,SHARP_E00765
    0007,SHARP_E00140
    0007,SHARP_E00141
    0008,SHARP_E00639
    0008,SHARP_E00640
    0009,SHARP_E00147
    0009,SHARP_E01907
    0010,SHARP_E00045
    0010,SHARP_E00044
    0011,SHARP_E00714
    0011,SHARP_E00713
    0013,SHARP_E00766
    0013,SHARP_E00767
    0014,SHARP_E00475
    0015,SHARP_E00741
    0015,SHARP_E00742
    0016,SHARP_E00009
    0016,SHARP_E00010
    0017,SHARP_E00643
    0017,SHARP_E00644
    0019,SHARP_E00245
    0020,SHARP_E00471
    0021,SHARP_E00033
    0022,SHARP_E00651
    0022,SHARP_E01648
    0023,SHARP_E00526
    0023,SHARP_E00522
    0024,SHARP_E00684
    0024,SHARP_E00685
    0025,SHARP_E00721
    0026,SHARP_E00628
    0026,SHARP_E00632
    0030,SHARP_E00351
    0030,SHARP_E00355
    0031,SHARP_E00740
    0031,SHARP_E00739
    0032,SHARP_E00496
    0032,SHARP_E00500
    0034,SHARP_E00058
    0034,SHARP_E00057
    0036,SHARP_E00407
    0037,SHARP_E00360
    0037,SHARP_E00363
    0038,SHARP_E00668
    0038,SHARP_E00667
    0040,SHARP_E00037
    0040,SHARP_E00038
    0041,SHARP_E00734
    0041,SHARP_E00733
    0042,SHARP_E00450
    0043,SHARP_E01651
    0043,SHARP_E00035
    0044,SHARP_E00552
    0044,SHARP_E00556
    0046,SHARP_E00705
    0047,SHARP_E00249
    0048,SHARP_E00022
    0048,SHARP_E00023
    0051,SHARP_E00652
    0051,SHARP_E00653
    0054,SHARP_E00728
    0055,SHARP_E00689
    0055,SHARP_E00688
    0059,SHARP_E00636
    0060,SHARP_E00712
    0062,SHARP_E00385
    0063,SHARP_E00680
    0063,SHARP_E00679
    0065,SHARP_E00708
    0065,SHARP_E00709
    0066,SHARP_E00726
    0067,SHARP_E00047
    0067,SHARP_E00046
    0068,SHARP_E00129
    0069,SHARP_E00265
    0069,SHARP_E00269
    0070,SHARP_E00600
    0070,SHARP_E00596
    0071,SHARP_E00029
    0073,SHARP_E00237
    0075,SHARP_E00297
    0075,SHARP_E00307
    0080,SHARP_E00139
    0080,SHARP_E00138
    0081,SHARP_E00719
    0081,SHARP_E00718
    0082,SHARP_E00457
    0082,SHARP_E00456
    0083,SHARP_E00724
    0083,SHARP_E00725
    0084,SHARP_E00459
    0084,SHARP_E00458
    0085,SHARP_E00731
    0085,SHARP_E00732
    0090,SHARP_E00112
    0090,SHARP_E00110
    0091,SHARP_E00564
    0091,SHARP_E00561
    0093,SHARP_E00743
    0094,SHARP_E01655
    0094,SHARP_E00681
    0095,SHARP_E00332
    0095,SHARP_E00336
    0098,SHARP_E00028
    0099,SHARP_E00039
    0101,SHARP_E00624
    0102,SHARP_E00241
    0104,SHARP_E00024
    0104,SHARP_E00025
    0105,SHARP_E00399
    0105,SHARP_E00403
    0107,SHARP_E00641
    0107,SHARP_E00642
    0110,SHARP_E00722
    0110,SHARP_E00723
    0112,SHARP_E00608
    0112,SHARP_E00605
    0113,SHARP_E00645
    0113,SHARP_E00646
    0114,SHARP_E00446
    0115,SHARP_E00398
    0115,SHARP_E00395
    0116,SHARP_E00229
    0116,SHARP_E00225
    0117,SHARP_E00006
    0117,SHARP_E00007
    0118,SHARP_E00735
    0118,SHARP_E00736
    0119,SHARP_E00699
    0119,SHARP_E00700
    0120,SHARP_E00620
    0120,SHARP_E00616
    0121,SHARP_E00748
    0121,SHARP_E00749
    0123,SHARP_E00649
    0123,SHARP_E00650
    0124,SHARP_E00730
    0124,SHARP_E00729
    0125,SHARP_E00026
    0125,SHARP_E00027
    0126,SHARP_E00745
    0126,SHARP_E00744
    0127,SHARP_E00032
    0128,SHARP_E00031
    0128,SHARP_E00030
    0129,SHARP_E00280
    0129,SHARP_E00283
    0131,SHARP_E00042
    0131,SHARP_E00043
    0132,SHARP_E00453
    


Filtering using Behavioral scores
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython2

    contraints = [('xnat:subjectData/SUBJECT_ID','LIKE','%'),
                      ('behavioral:scores/VocabScore', '>=', '36'),
                      'AND', ('xnat:subjectData/PROJECT', '=', 'FAST')
                 ]
    table1 = xnat.select('xnat:subjectData').where(contraints)
    table1.__len__()




.. parsed-literal::

    18



Downloading the selective data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lets start with download data for one subject

.. code:: ipython2

    subject = xnat.select.project('FAST').subject('0001')
    experiment = subject.experiment("SHARP_E00746")
    allscans = experiment.scans()
    allscans.download("/tmp", type='ALL', extract=False)




.. parsed-literal::

    '/tmp/FAST_0001_SHARP_E00746_scans_ALL.zip'



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
