# Copyright (C) 2018-2019 Intel Corporation
# SPDX-License-Identifier: Apache-2.0
#

ie_add_sample(NAME Camera
              SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/OpencvCapture.cpp"
#              HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/object_detection_demo_ssd_async.hpp"
              OPENCV_DEPENDENCIES highgui videoio imgproc)
