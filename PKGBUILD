pkgdesc="ROS - tools for recording from and playing back to ROS topics."
url='http://www.ros.org/'

pkgname='ros-groovy-rosbag'
pkgver='1.9.50'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-roscpp
  ros-groovy-catkin
  ros-groovy-genmsg
  ros-groovy-topic-tools
  ros-groovy-roscpp-serialization
  ros-groovy-rostime
  ros-groovy-genpy
  ros-groovy-roslib
  ros-groovy-rosconsole
  ros-groovy-rosunit
  ros-groovy-rospy
  ros-groovy-cpp-common
  ros-groovy-xmlrpcpp
  ros-groovy-rostest
  ros-groovy-langs-dev
  ros-groovy-roscpp-traits
  ros-groovy-rosgraph-msgs
  bzip2
  boost
  python2-imaging)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/rosbag ]; then
    cd ${srcdir}/rosbag
    git fetch origin --tags
    git reset --hard release/groovy/rosbag/${pkgver}-0
  else
    git clone -b release/groovy/rosbag/${pkgver}-0 git://github.com/ros-gbp/ros_comm-release.git ${srcdir}/rosbag
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/rosbag
  cmake ${srcdir}/rosbag -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
