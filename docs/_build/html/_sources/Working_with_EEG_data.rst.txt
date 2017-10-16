Working with EEG data
==============================

.. code:: ipython2

    import pyxnat
    import os
    
    # connect to XNAT instance
    from pyxnat import Interface
    xnat = Interface(server='http://sharp.bidmc.harvard.edu:8080',  cachedir='/tmp')
    xnat.select.projects().get()

.. code:: ipython2

    project = xnat.select.project('EEG_SHARP')

.. code:: ipython2

    subject = project.subject('0001')

.. code:: ipython2

    experiments = subject.experiments()

.. code:: ipython2

    for list_experiment in experiments:
        files = list_experiment.resources().files()
        for fl in files:
            print (fl)

