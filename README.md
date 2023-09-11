# ros3vfd-log-info

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ajelenak/ros3vfd-log-info/HEAD?labpath=ros3vfd-log-info.ipynb)

The [HDF5 library](https://www.hdfgroup.org/solutions/hdf5/) includes a read-only virtual file driver for the AWS Simple Storage Service (S3) or any S3-compatible storage system. The driver, called Read-only S3 (_ROS3_), can be used to read data from an HDF5 file as S3 object. Since the library's release 1.14.1, the driver can log various information related to its S3 operations. These data can be useful when deciding which HDF5 file or library features to use for improved data access performance.

This repository contains a simple dashboard for the driver's log data about S3 (HTTP range GET) requests. These requests represent individual data read operations by the library and directly affect performance. It takes a ROS3 log file and displays statistics and two plots about the HTTP requests performed to read the data. The dashboard is implemented as a [Panel web app](https://panel.holoviz.org/) in a [Jupyter notebook](https://jupyter-notebook.readthedocs.io/en/latest/). Due to the current Panel limitation, only log files less than 10 megabytes can be used. The easiest way to use it is via the Binder service at this link.

## How to Get ROS3 Logs

To generate log information requires buiding the HDF5 library and ROS3 driver because it is not currently possible to enable this logging any other way. After obtaining the library source code, enable ROS3 logging by changing `0` to `1` in the `#define S3COMMS_DEBUG 0` line of the _H5FDs3comms.c_ file. After the change, build the library with the ROS3 driver according to the instructions. Any time the ROS3 driver is used the logging information will be printed to _stdout_. Redirect it to a file and you have something to upload to the dashboard.

## Two Ways to Run the Dashboard

The dashboard can be run as a typical Jupyter notebook, or a standalone app in a browser with this command: `panel serve ros3vfd-log-info.ipynb --show`.
