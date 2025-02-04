.. 8mile-render documentation master file, created by
   sphinx-quickstart on Fri Aug 12 08:58:15 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to 8mile-render's documentation!
========================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

8mile allow users to renderer time series data and especially financial ones.

Installation
------------

.. code-block:: bash
   :caption: EXT:installation
   
   pip3 install git+https://github.com/theophane-droid/8miles-render


Example 
-------

Use a RabbitRenderer to print time series in tensorboard :

.. code-block:: python3
   :caption: EXT:rabbit_renderer.py

   from datetime import datetime
   import pandas as pd
   from Hmilerender.RabbitRenderer import RabbitRenderer

   def fill_renderer(data, renderer):
    # we fill the renderer with data rows
      for index, row in data.iterrows():
         date = datetime.strptime(row["Date"], "%Y-%m-%d")
         renderer.append("open", row["open"], date)
         renderer.append("close", row["close"], date)
         renderer.append("high", row["high"], date)
         renderer.append("low", row["low"], date)
         renderer.append("volume", row["volume"], date)
         renderer.append("exit", row["exit"], date)
         renderer.append("long", row["long"], date)
         renderer.append("short", row["short"], date)
         renderer.append("money", row["money"], date)

   # we create a renderer object
   renderer = RabbitRenderer('logs/')
   # we read data
   data = pd.read_csv('data/data.csv')
   # we fill renderer
   fill_renderer(data, renderer)
   # we launch renderer
   renderer.render() 
   # then we increment tensorboard step
   renderer.next_step()
   # we refill the renderer
   fill_renderer(data, renderer)
   # we launch renderer
   renderer.render()

Result in tensorboard :

.. image:: img/tensorboard01.PNG
  :width: 600
  :alt: Alternative text   
   

Implemented Renderer
--------------------

.. autoclass:: Hmilerender.RabbitRenderer.RabbitRenderer
   :members:
   :inherited-members:



Core classes
------------

.. autoclass:: Hmilerender.Renderer.Renderer
   :members:
   :inherited-members:

.. autoclass:: Hmilerender.Renderer.RenderTask
   :members:
   :inherited-members:

Exceptions
----------
.. autoclass:: Hmilerender.Exception.ColumnNameDoesNotExists
   :members:
   :inherited-members:


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
