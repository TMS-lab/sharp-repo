MRIQC
==============

MRIQC extracts no-reference IQMs (image quality metrics) from
structural (T1w and T2w) and functional MRI (magnetic resonance imaging)
data.

MRIQC is an open-source project, developed under the following
software engineering principles:

#. **Modularity and integrability**: MRIQC implements a
   `nipype <http://nipype.readthedocs.io>`_ workflow to integrate modular 
   sub-workflows that rely upon third party software toolboxes such as 
   FSL, ANTs and AFNI.

#. **Minimal preprocessing**: the MRIQC workflows should be as minimal
   as possible to estimate the IQMs on the original data or their minimally
   processed derivatives.

#. **Interoperability and standards**: MRIQC follows the the `brain imaging data structure
   (BIDS) <http://bids.neuroimaging.io>`_, and it adopts the `BIDS-App
   <http://bids-apps.neuroimaging.io>`_ standard.
   
#. **Reliability and robustness**: the software undergoes frequent vetting sprints
   by testing its robustness against data variability (acquisition parameters,
   physiological differences, etc.) using images from `OpenfMRI <https://openfmri.org>`_.
   Its reliability is permanently checked and maintained with 
   `CircleCI <https://circleci.com/gh/poldracklab/mriqc>`_.


MRIQC is part of the MRI image analysis and reproducibility platform offered by
the CRN. This pipeline derives from, and is heavily influenced by, the
`PCP Quality Assessment Protocol <http://preprocessed-connectomes-project.github.io/quality-assessment-protocol>`_.

SHARP Data Reposts
====================
.. raw:: html
   :file: ../mriqc/reports/sub-0001_T1w.html
.. raw:: html   
   :file: ../mriqc/reports/sub-0001_T1w.html
.. raw:: html   
   :file: ../mriqc/reports/sub-0001_task-resting_run-01_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0001_task-resting_run-02_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0001_task-resting_run-03_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0002_T1w.html
.. raw:: html
   :file: ../mriqc/reports/sub-0002_task-resting_run-01_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0002_task-resting_run-02_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0002_task-resting_run-03_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0003_T1w.html
.. raw:: html
   :file: ../mriqc/reports/sub-0003_task-resting_run-01_bold.html
.. raw:: html
   :file: ../mriqc/reports/sub-0003_task-resting_run-02_bold.html
.. raw:: html
   :file:../mriqc/reports/sub-0003_task-resting_run-03_bold.html
