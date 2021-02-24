Why MLflow?
-----------

1. **There are a myriad tools.** Hundreds of open source tools cover each phase of the ML lifecycle, from data preparation to model training. However, unlike traditional software development, where teams select one tool for each phase, in ML you usually want to try every available tool (e.g. algorithm) to see whether it improves results. ML developers thus need to use and productionize dozens of libraries.

2. **It’s hard to track experiments.** Machine learning algorithms have dozens of configurable parameters, and whether you work alone or on a team, it is difficult to track which parameters, code, and data went into each experiment to produce a model.

3. **It’s hard to reproduce results.** Without detailed tracking, teams often have trouble getting the same code to work again. Whether you are a data scientist passing your training code to an engineer for use in production, or you are going back to your past work to debug a problem, reproducing steps of the ML workflow is critical.

4. **It’s hard to deploy ML.** Moving a model to production can be challenging due to the plethora of deployment tools and environments it needs to run in (e.g. REST serving, batch inference, or mobile apps). There is no standard way to move models from any library to any of these tools, creating a new risk with each new deployment.

Because of these challenges, it is clear that ML development has to evolve a lot to become as robust, predictable and wide-spread as traditional software development. To this end, many organizations have started to build internal machine learning platforms to manage the ML lifecycle. However, even these internal platforms are limited: typical ML platforms only support a small set of built-in algorithms, or a single ML library, and they are tied to each company’s infrastructure.

Installing
----------
Install MLflow from PyPI via ``pip install mlflow``

MLflow requires ``conda`` to be on the ``PATH`` for the projects feature.

Overview
--------

![MLflow Components](https://databricks.com/wp-content/uploads/2018/06/mlflow.png)

MLflow is an open machine learning platform to streamline machine learning development, including tracking experiments, packaging code
into reproducible runs, and sharing and deploying models. MLflow offers a set of lightweight APIs that can be
used with any existing machine learning application or library (TensorFlow, PyTorch, XGBoost, etc), wherever you
currently run ML code (e.g. in notebooks, standalone applications or the cloud). MLflow's core components are:

* **MLflow Tracking**: An API to log parameters, code, and
  results in machine learning experiments and compare them using an interactive UI.
* **MLflow Projects**: A code packaging format for reproducible
  runs using Conda and Docker, so you can share your ML code with others.
* **MLflow Models**: A model packaging format and tools that let
  you easily deploy the same model (from any ML library) to batch and real-time scoring on platforms such as
  Docker, Apache Spark, Azure ML and AWS SageMaker.
  
MLflow Tracking
---------------

MLflow Tracking is an API and UI for logging parameters, code versions, metrics and output files when running your machine learning code to later visualize them. With a few simple lines of code, you can track parameters, metrics, and artifacts:
  ```
      import mlflow

      # Log parameters (key-value pairs)
      mlflow.log_param("num_dimensions", 8)
      mlflow.log_param("regularization", 0.1)

      # Log a metric; metrics can be updated throughout the run
      mlflow.log_metric("accuracy", 0.1)
      ...
      mlflow.log_metric("accuracy", 0.45)

      # Log artifacts (output files)
      mlflow.log_artifact("roc.png")
      mlflow.log_artifact("model.pkl")
  ```

![MLflow Tracking UI](https://databricks.com/wp-content/uploads/2018/06/mlflow-web-ui.png)

MLflow Projects
---------------

MLflow Projects provide a standard format for packaging reusable data science code. Each project is simply a directory with code or a Git repository, and uses a descriptor file to specify its dependencies and how to run the code. A MLflow Project is defined by a simple YAML file called MLproject.

  ```
    name: My Project
    conda_env: conda.yaml
    entry_points:
      main:
        parameters:
          data_file: path
          regularization: {type: float, default: 0.1}
        command: "python train.py -r {regularization} {data_file}"
      validate:
        parameters:
          data_file: path
        command: "python validate.py {data_file}"
  ```

Projects can specify their dependencies through a Conda environment. A project may also have multiple entry points for invoking runs, with named parameters. You can run projects using the mlflow run command-line tool, either from local files or from a Git repository:

  ```
    mlflow run example/project -P alpha=0.5

    mlflow run git@github.com:databricks/mlflow-example.git -P alpha=0.5
  ```
MLflow will automatically set up the right environment for the project and run it. In addition, if you use the MLflow Tracking API in a Project, MLflow will remember the project version executed (that is, the Git commit) and any parameters. You can then easily rerun the exact same code.

The project format makes it easy to share reproducible data science code, whether within your company or in the open source community. Coupled with MLflow Tracking, MLflow Projects provides great tools for reproducibility, extensibility, and experimentation.

MLflow Models
-------------

MLflow Models is a convention for packaging machine learning models in multiple formats called “flavors”. Each MLflow Model is saved as a directory containing arbitrary files and an MLmodel descriptor file that lists the flavors it can be used in.

  ```
    time_created: 2018-02-21T13:21:34.12
    flavors:
      sklearn:
        sklearn_version: 0.19.1
        pickled_model: model.pkl
      python_function:
        loader_module: mlflow.sklearn
        pickled_model: model.pkl
  ```

In this example, the model can be used with tools that support either the sklearn or python_function model flavors.

MLflow provides tools to deploy many common model types to diverse platforms. For example, any model supporting the python_function flavor can be deployed to a Docker-based REST server, to cloud platforms such as Azure ML and Amazon SageMaker, and as a user-defined function in Apache Spark for batch and streaming inference. If you output MLflow Models as artifacts using the Tracking API, MLflow will also automatically remember which Project and run they came from.

Launching the Tracking UI
-------------------------
The MLflow Tracking UI will show runs logged in ``./mlruns`` at `<http://localhost:5000>`_.
Start it with::

    mlflow ui

**Note:** Running ``mlflow ui`` from within a clone of MLflow is not recommended.

Saving and Serving Models
-------------------------
To illustrate managing models, the ``mlflow.sklearn`` package can log scikit-learn models as
MLflow artifacts and then load them again for serving. There is an example training application in
``examples/sklearn_logistic_regression/train.py`` that you can run as follows::

    $ python examples/sklearn_logistic_regression/train.py
    Score: 0.666
    Model saved in run <run-id>

    $ mlflow models serve --model-uri runs:/<run-id>/model

    $ curl -d '{"columns":[0],"index":[0,1],"data":[[1],[-1]]}' -H 'Content-Type: application/json'  localhost:5000/invocations

Best Practices for Hyperparameter Tuning with MLflow
----------------------------------------------------

What to track in a run for a model 
* **Hyperparameters:** all vs ones being tuned 
* **Metric(s):** training & validation, loss & objective function
* **Tags:** simple metadata 
* **Artifacts:** serialized model (.pkl, .h5, .hdf5, .pb, .pt, etc), large metadata (.json, .csv, .xlsx, etc)

Tune full pipeline, not 1 model.

Documentation
-------------
Official documentation for MLflow can be found at https://mlflow.org/docs/latest/index.html.

References
----------

1. https://www.slideshare.net/databricks/introduction-fo-mlflow
2. https://databricks.com/blog/2018/06/05/introducing-mlflow-an-open-source-machine-learning-platform.html
3. https://github.com/mlflow/mlflow
4. https://www.slideshare.net/databricks/best-practices-for-hyperparameter-tuning-with-mlflow
