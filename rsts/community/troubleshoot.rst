.. _troubleshoot:

Troubleshooting Guide
---------------------

.. admonition:: Why have we crafted this guide?

    Let go of overthinking; peep into this page.

We've been working diligently to help users sort out issues. 

Here are a couple of techniques we believe would help you jump out of the pandora box quickly! 

* If the issue is related to the ``make start`` command:
    - ``make start`` usually gets completed within five minutes (could take longer if you aren't in the United States).
    - If ``make start`` results in a timeout issue:
       .. code-block:: bash
  
         Starting Flyte sandbox
         Waiting for Flyte to become ready...
         Error from server (NotFound): deployments.apps "datacatalog" not found
         Error from server (NotFound): deployments.apps "flyteadmin" not found
         Error from server (NotFound): deployments.apps "flyteconsole" not found
         Error from server (NotFound): deployments.apps "flytepropeller" not found
         Timed out while waiting for the Flyte deployment to start
       
       You can run ``make teardown`` followed by the ``make start`` command.

    - If the ``make start`` command isn't proceeding by any chance, check the pods' statuses by run this command  

      ::

       docker exec flyte-sandbox kubectl get po -A
    - If you think a pod's crashing or getting evicted by any chance, describe the pod by running the command which gives detailed overview of pod's status

      ::

       docker exec flyte-sandbox kubectl describe po <pod-name> -n flyte 

    - If Kubernetes reports a disk pressure issue: (node.kubernetes.io/disk-pressure)
    
      - Check the memory stats of the docker container using the command ``docker exec flyte-sandbox df -h``.
      - Prune the images and volumes. 
      - Given there's less than 10% free disk space, Kubernetes, by default, throws the disk pressure error.

.. NOTE::

      More coming soon. Stay tuned 👀

    
If the issue is still bugging you, contact us on `Slack <http://flyte-org.slack.com/>`__. 
