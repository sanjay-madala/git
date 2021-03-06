# Copyright (c) 2006-2008 MySQL AB, 2008, 2009 Sun Microsystems, Inc.
# Use is subject to license terms.
# 
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 2 of the License.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA

INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include
                    ${CMAKE_SOURCE_DIR}/libmysqld/include
                    ${CMAKE_SOURCE_DIR}/regex
                    ${CMAKE_SOURCE_DIR}/zlib
                    ${CMAKE_SOURCE_DIR}/tests
                    ${CMAKE_SOURCE_DIR}/extra/yassl/include)

# Currently does not work with DBUG, there are missing symbols reported.
IF(WIN32)
  ADD_DEFINITIONS(-DUSE_TLS)
ENDIF(WIN32)

ADD_DEFINITIONS(-DEMBEDDED_LIBRARY)

ADD_EXECUTABLE(mysql_embedded ../../client/completion_hash.cc
               ../../client/mysql.cc ../../client/readline.cc
               ../../client/sql_string.cc)
TARGET_LINK_LIBRARIES(mysql_embedded debug dbug strings mysys vio yassl taocrypt regex ws2_32)
TARGET_LINK_LIBRARIES(mysql_embedded libmysqld)

ADD_EXECUTABLE(mysqltest_embedded ../../client/mysqltest.cc)
TARGET_LINK_LIBRARIES(mysqltest_embedded debug dbug strings mysys vio yassl taocrypt regex ws2_32)
TARGET_LINK_LIBRARIES(mysqltest_embedded libmysqld)

ADD_EXECUTABLE(mysql_client_test_embedded ../../tests/mysql_client_test.c)
TARGET_LINK_LIBRARIES(mysql_client_test_embedded debug dbug strings mysys vio yassl taocrypt regex ws2_32)
TARGET_LINK_LIBRARIES(mysql_client_test_embedded libmysqld)
