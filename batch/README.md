## Goals

Provide a reasonably flexible abstraction (e.g. so someone could extend it to other targets like AWS in the future if they wanted) for executing lots of tests (tasks) for an optimization experiment (job) at scale (parallel) and remotely.

This would be of most benefit for executing longer running benchmarks (e.g. TPC-C, TPC-H on larger systems).

Data visualization and analysis is still expected to be driven from a notebook, but actual benchmark execution should be asynchronous from it.

## Expected Notebook usage
```
From mlos.batch import compute_pool, storage_client, job, task, config

cfg = config('config_path')
comp_pool = ComputePool(cfg.compute_pool.local)

job = Job(comp_pool, cfg)
job.start()



```

## Python Abstractions

class ComputePool: 

    """The ComputePool class setup the required to create a place 

    to run a "Job".   

    """ 

    def __init__(self, config, batch_service_client): 

        """Initializes the compute pool based on the config for the nodes  

        """ 

 

    def get_compute_pool(self): 

        """get the infomation on compute pool 

        """ 

 


class Job: 

    """Represents a full experiment run and kicks off the 

    driver/jobManagerTask using the configs setup by the notebook. 

    """ 
 

    def __init__(self, compute_pool, config): 

        """Initializes the job with id and compute pool 

        """ 

        self.job_id = uuid.uuid4().hex 
 

    def start(self): 

        """start a job. This will triggers a job in the env job will run  

        """ 
 
    def stop(self): 

        """Stop a job. This will hard stop a job in the env job will run  

        """ 

    def status(self):

        """Get the status of the job

        """

    def _build_driver(self): 

        """Builds a driver container 

        """ 
 

    def _build_worker(self): 

        """Builds a worker container 

        """ 
 

    def _launch_driver(self): 

        """Launches driver container 

        """ 
 

    def _launch_driver(self): 

        """Launches a worker container 

        """ 
 

    def _shutdown_driver(self): 

        """Shutdown a driver container 

        """ 


    def _shutdown_worker(self): 

        """Shutdown a worker container 

        """ 

         


class Task: 

    """Represents a task that can be either driver or worker 

    """ 

 

    def __init__(self, config): 

        """Initializes for particular config 

        """ 

        self.task_id = uuid.uuid4().hex 
 

    def build_task(self): 

        """Builds a task container 

        """ 
 

    def launch_task(self): 

        """Launches a task 

        """ 
 

    def get_status(self): 

        """Get status from the container 

        """ 

    def shutdown_task(self): 

        """Shutdown the task container 

        """ 

 

 

class storage_client: 

    """Represents storage where results and input can be collected from 

    """ 
 

    def __init__(self, config): 

        """Initializes for particular config and creates a directory structure  

        at location provided in the config. 

        """ 
 

    def read_data(self, loc): 

        """Read data from the location 

        """ 
 

    def write_data(self, loc): 

        """Write data on to location 

        """ 

 

    def reset(self): 

        """Reset the the directory structure to start a a fresh 

        """ 

 
Config: 

    """A directory contains the configuration essentials 

    """ 
    Compute_pool
        local.yaml
        azure_batch.yaml
        cloudlab.yaml
        instance_type

    Task
        driver/Dockerfile
        worker
            /Dockerfile
            /dbms

    env.yaml # for env variables

 
Container_scripts: 

    """A directory structure to keep scripts related to benchmark setup or parse that's going to be used in dockerfile
    """
    oltpbench.py
    postgres.py
    sync.py
    parse_result.py




 