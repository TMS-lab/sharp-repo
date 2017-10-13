Node: write_log (utility)
=========================

 Hierarchy : log_done_scan_task-resting_run-03.write_log
 Exec ID : write_log

Original Inputs
---------------

* function_str : def write_to_log(workflow, log_dir, index, inputs, scan_id ):
    """
    Method to write into log file the status of the workflow run.
    """

    import os
    import CPAC
    from nipype import logging
    iflogger = logging.getLogger('interface')

    version = CPAC.__version__

    subject_id = os.path.basename(log_dir)

    if scan_id == None:
        scan_id = "scan_anat"

    strategy = ""

    import time
    import datetime
    ts = time.time()

    stamp = datetime.datetime.fromtimestamp(ts).strftime('%Y-%m-%d %H:%M:%S')
    try:
        if workflow!= 'DONE':
            wf_path = os.path.dirname((os.getcwd()).split(workflow)[1]).strip("/")

            if wf_path and wf_path != "":
                if '/' in wf_path:
                    scan_id, strategy = wf_path.split('/',1)
                    scan_id = scan_id.strip('_')
                    strategy = strategy.replace("/","")
                else:
                    scan_id = wf_path.strip('_')

            file_path = os.path.join(log_dir, scan_id, workflow)

            try:
                os.makedirs(file_path)
            except Exception:
                iflogger.info("filepath already exist, filepath- %s, curr_dir - %s"%(file_path, os.getcwd()))

        else:
            file_path = os.path.join(log_dir, scan_id)
    except Exception:
        print "ERROR in write log"
        raise

    try:
        os.makedirs(file_path)
    except Exception:
        iflogger.info("filepath already exist, filepath- %s, curr_dir - %s"%(file_path, os.getcwd()))

    out_file = os.path.join(file_path, 'log_%s.yaml'%strategy)

    f = open(out_file, 'w')


    print >>f, "version : %s"%(str(version))
    print >>f, "timestamp: %s"%(str(stamp))
    print >>f, "pipeline_index: %d"%(index) 
    print >>f, "subject_id: %s"%(subject_id)
    print >>f, "scan_id: %s"%(scan_id)
    print >>f, "strategy: %s"%(strategy)
    print >>f, "workflow_name: %s"%(workflow)



    iflogger.info("CPAC custom log :")

    if isinstance(inputs, list):
        inputs = inputs[0]

    if os.path.exists(inputs):

        print >>f,  "wf_status: DONE"

        iflogger.info(" version - %s, timestamp -%s, subject_id -%s, scan_id - %s, strategy -%s, workflow - %s, status -%s"\
                      %(str(version), str(stamp), subject_id, scan_id,strategy,workflow,'COMPLETED') )

    else:

        iflogger.info(" version - %s, timestamp -%s, subject_id -%s, scan_id - %s, strategy -%s, workflow - %s, status -%s"\
                      %(str(version), str(stamp), subject_id, scan_id,strategy,workflow,'ERROR') )

        print>>f, "wf_status: ERROR"

    f.close()

    #os.system("/home2/haipan/tmp/C-PAC/scripts/log_py2js.py %s %s"%(out_file, log_dir))   ###

    return out_file

* ignore_exception : False
* index : 1
* inputs : /outputs/log/sub-0001_ses-1
* log_dir : /outputs/log/sub-0001_ses-1
* scan_id : scan_task-resting_run-03
* workflow : DONE

Execution Inputs
----------------

* function_str : def write_to_log(workflow, log_dir, index, inputs, scan_id ):
    """
    Method to write into log file the status of the workflow run.
    """

    import os
    import CPAC
    from nipype import logging
    iflogger = logging.getLogger('interface')

    version = CPAC.__version__

    subject_id = os.path.basename(log_dir)

    if scan_id == None:
        scan_id = "scan_anat"

    strategy = ""

    import time
    import datetime
    ts = time.time()

    stamp = datetime.datetime.fromtimestamp(ts).strftime('%Y-%m-%d %H:%M:%S')
    try:
        if workflow!= 'DONE':
            wf_path = os.path.dirname((os.getcwd()).split(workflow)[1]).strip("/")

            if wf_path and wf_path != "":
                if '/' in wf_path:
                    scan_id, strategy = wf_path.split('/',1)
                    scan_id = scan_id.strip('_')
                    strategy = strategy.replace("/","")
                else:
                    scan_id = wf_path.strip('_')

            file_path = os.path.join(log_dir, scan_id, workflow)

            try:
                os.makedirs(file_path)
            except Exception:
                iflogger.info("filepath already exist, filepath- %s, curr_dir - %s"%(file_path, os.getcwd()))

        else:
            file_path = os.path.join(log_dir, scan_id)
    except Exception:
        print "ERROR in write log"
        raise

    try:
        os.makedirs(file_path)
    except Exception:
        iflogger.info("filepath already exist, filepath- %s, curr_dir - %s"%(file_path, os.getcwd()))

    out_file = os.path.join(file_path, 'log_%s.yaml'%strategy)

    f = open(out_file, 'w')


    print >>f, "version : %s"%(str(version))
    print >>f, "timestamp: %s"%(str(stamp))
    print >>f, "pipeline_index: %d"%(index) 
    print >>f, "subject_id: %s"%(subject_id)
    print >>f, "scan_id: %s"%(scan_id)
    print >>f, "strategy: %s"%(strategy)
    print >>f, "workflow_name: %s"%(workflow)



    iflogger.info("CPAC custom log :")

    if isinstance(inputs, list):
        inputs = inputs[0]

    if os.path.exists(inputs):

        print >>f,  "wf_status: DONE"

        iflogger.info(" version - %s, timestamp -%s, subject_id -%s, scan_id - %s, strategy -%s, workflow - %s, status -%s"\
                      %(str(version), str(stamp), subject_id, scan_id,strategy,workflow,'COMPLETED') )

    else:

        iflogger.info(" version - %s, timestamp -%s, subject_id -%s, scan_id - %s, strategy -%s, workflow - %s, status -%s"\
                      %(str(version), str(stamp), subject_id, scan_id,strategy,workflow,'ERROR') )

        print>>f, "wf_status: ERROR"

    f.close()

    #os.system("/home2/haipan/tmp/C-PAC/scripts/log_py2js.py %s %s"%(out_file, log_dir))   ###

    return out_file

* ignore_exception : False
* index : 1
* inputs : /outputs/log/sub-0001_ses-1
* log_dir : /outputs/log/sub-0001_ses-1
* scan_id : scan_task-resting_run-03
* workflow : DONE

Execution Outputs
-----------------

* out_file : /outputs/log/sub-0001_ses-1/scan_task-resting_run-03/log_.yaml

Runtime info
------------

* duration : 0.01366
* hostname : aa6690c340ff

Environment
~~~~~~~~~~~

* ANTSPATH : /opt/ants/bin/
* DYLD_FALLBACK_LIBRARY_PATH : /opt/afni
* FSLBROWSER : /etc/alternatives/x-www-browser
* FSLDIR : /usr/share/fsl/5.0
* FSLMULTIFILEQUIT : TRUE
* FSLOUTPUTTYPE : NIFTI_GZ
* FSLTCLSH : /usr/bin/tclsh
* FSLWISH : /usr/bin/wish
* HOME : /root
* HOSTNAME : aa6690c340ff
* ITK_GLOBAL_DEFAULT_NUMBER_OF_THREADS : 1
* LD_LIBRARY_PATH : /usr/lib/fsl/5.0:
* MKL_NUM_THREADS : 1
* OMP_NUM_THREADS : 1
* PATH : /code:/opt/c3d/bin:/opt/ants/bin:/opt/afni:/usr/share/fsl/5.0/bin:/usr/local/bin/miniconda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

