# Raspberry-Pi4   Ref:https://qengineering.eu/install-opencv-4.2-on-raspberry-pi-4.html

# DeepLearning
# Installation OpenCV4.2

$ sudo apt-get update
$ sudo apt-get upgrade

$ sudo apt-get clean
$ sudo apt-get autoremove

# Dépendance


$ sudo apt-get install build-essential cmake git unzip pkg-config
$ sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
$ sudo apt-get install libgtk2.0-dev libcanberra-gtk*
$ sudo apt-get install libxvidcore-dev libx264-dev libgtk-3-dev
$ sudo apt-get install python3-dev python3-numpy python3-pip
$ sudo apt-get install python-dev python-numpy
$ sudo apt-get install libtbb2 libtbb-dev libdc1394-22-dev
$ sudo apt-get install libv4l-dev v4l-utils
$ sudo apt-get install libjasper-dev libopenblas-dev libatlas-base-dev libblas-dev
$ sudo apt-get install liblapack-dev gfortran
$ sudo apt-get install gcc-arm*
$ sudo apt-get install protobuf-compiler

# Download

$ cd ~
$ wget -O opencv.zip https://github.com/opencv/opencv/archive/4.2.0.zip
$ wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.2.0.zip
$ unzip opencv.zip
$ unzip opencv_contrib.zip


$ mv opencv-4.2.0 opencv
$ mv opencv_contrib-4.2.0 opencv_contrib

# Creation d'un environnement virtuel
$ sudo pip3 install virtualenv
$ sudo pip3 install virtualenvwrapper


$ echo "export WORKON_HOME=$HOME/.virtualenvs" >> ~/.bashrc
$ echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc
$ source ~/.bashrc
$ mkvirtualenv cv420

# Compilation 
$ cd ~/opencv/
$ mkdir build
$ cd build


$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
        -D ENABLE_NEON=ON \
        -D ENABLE_VFPV3=ON \
        -D WITH_OPENMP=ON \
        -D BUILD_TIFF=ON \
        -D WITH_FFMPEG=ON \
        -D WITH_GSTREAMER=ON \
        -D WITH_TBB=ON \
        -D BUILD_TBB=ON \
        -D BUILD_TESTS=OFF \
        -D WITH_EIGEN=OFF \
        -D WITH_V4L=ON \
        -D WITH_LIBV4L=ON \
        -D WITH_VTK=OFF \
        -D OPENCV_EXTRA_EXE_LINKER_FLAGS=-latomic \
        -D OPENCV_ENABLE_NONFREE=ON \
        -D INSTALL_C_EXAMPLES=OFF \
        -D INSTALL_PYTHON_EXAMPLES=OFF \
        -D BUILD_NEW_PYTHON_SUPPORT=ON \
        -D BUILD_opencv_python3=TRUE \
        -D OPENCV_GENERATE_PKGCONFIG=ON \
        -D BUILD_EXAMPLES=OFF ..

# Reservation de la mémoire (4096M)
$ sudo nano /etc/dphys-swapfile


$ sudo /etc/init.d/dphys-swapfile stop
$ sudo /etc/init.d/dphys-swapfile start
# Compilation et installation

$ make -j4
$ sudo make install
$ sudo ldconfig
$ sudo apt-get update

# Restauration mémoire

$ sudo nano /etc/dphys-swapfile

set CONF_SWAPSIZE=100 with the Nano text editor

$ cd ~
$ rm opencv.zip
$ rm opencv_contrib.zip
$ reboot



$ cd ~/.virtualenvs/cv420/lib/python3.7/site-packages
$ ln -s /usr/local/lib/python3.7/site-packages/cv2/python-3.7/cv2.cpython-37m-arm-linux-gnueabihf.so
$ cd ~

# Example d'affichage de version OpenCV (c++)

#include <opencv2/opencv.hpp>
int main(void)
{
    std::cout << "OpenCV version : " << cv::CV_VERSION << endl;
    std::cout << "Major version : " << cv::CV_MAJOR_VERSION << endl;
    std::cout << "Minor version : " << cv::CV_MINOR_VERSION << endl;
    std::cout << "Subminor version : " << cv::CV_SUBMINOR_VERSION << endl;
    std::cout << cv::getBuildInformation() << std::endl;
}






