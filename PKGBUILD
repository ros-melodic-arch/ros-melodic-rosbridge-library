pkgdesc="ROS - The core rosbridge package, repsonsible for interpreting JSON and
performing the appropriate ROS action, like subscribe, publish, call service,
and interact with params."
url='https://wiki.ros.org/rosbridge_library'

pkgname='ros-melodic-rosbridge-library'
pkgver='0.11.6'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=2
license=('BSD')

ros_makedepends=(
	ros-melodic-catkin
    ros-melodic-std-msgs
    ros-melodic-geometry-msgs
    ros-melodic-message-generation
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
    python-pillow
    python-bson
)

ros_depends=(
    ros-melodic-rospy
    ros-melodic-roscpp
    ros-melodic-rosgraph
    ros-melodic-rosservice
    ros-melodic-rostopic
    ros-melodic-std-msgs
    ros-melodic-geometry-msgs
    ros-melodic-message-runtime
)

depends=(
	${ros_depends[@]}
    python-pillow
    python-bson
)

_dir="rosbridge_suite-${pkgver}/rosbridge_library"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/RobotWebTools/rosbridge_suite/archive/${pkgver}.tar.gz")
sha256sums=('ac7a4fc4c3dd8866e90aacf5dafc53b9b0ca9bd6676f141e0ecd9a3b7fc694a6')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Fix Python2/Python3 conflicts.
	/usr/share/ros-build-tools/fix-python-scripts.sh -v 3 ${srcdir}/${_dir}

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCMAKE_BUILD_TYPE=Release \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
		-DPYTHON_EXECUTABLE=/usr/bin/python3 \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
