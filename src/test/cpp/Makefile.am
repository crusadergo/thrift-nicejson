
GENCPP0_test0 = \
gen-cpp/test0_constants.cpp \
gen-cpp/test0_constants.h \
gen-cpp/test0_types.cpp \
gen-cpp/test0_types.h

GENCPP_test = \
gen-cpp/test_constants.cpp \
gen-cpp/test_constants.h \
gen-cpp/test_types.cpp \
gen-cpp/test_types.h

GENCPP_TYPELIB_test = \
gen-cpp-typelib/test_typelib.cpp \
gen-cpp-typelib/test_typelib.h


GENCPP_TYPELIB_test0 = \
gen-cpp-typelib/test0_typelib.cpp \
gen-cpp-typelib/test0_typelib.h

GENCPP_TYPELIB_plugin = \
gen-cpp-typelib/plugin_typelib.cpp \
gen-cpp-typelib/plugin_typelib.h

GENJSON_test = gen-json/test.json
GENJSON_test0 = gen-json/test0.json
GENJSON_plugin = gen-json/plugin.json

BUILT_SOURCES = \
$(GENCPP0_test0) $(GENCPP_test) \
$(GENCPP_TYPELIB_test) \
$(GENCPP_TYPELIB_test0) \
$(GENCPP_TYPELIB_plugin) \
$(GENJSON0_test0) \
$(GENJSON_test) \
$(GENJSON_plugin)

CLEANFILES = $(BUILT_SOURCES)

check_PROGRAMS = test1 test2

test1_SOURCES = test1.cpp $(BUILT_SOURCES)
test1_LDFLAGS = -Wl,-rpath -Wl,$(thrift_LIBDIR)
test1_LDADD = ../../lib/cpp/libnicejson.a $(thrift_LIBS) $(BOOST_FILESYSTEM_LDADD) $(BOOST_SYSTEM_LDADD)
test1_CXXFLAGS = -I../../lib/cpp $(thrift_CFLAGS) $(AM_CXXFLAGS)

test2_SOURCES = test2.cpp $(GENCPP_test)
test2_LDFLAGS = -Wl,-rpath -Wl,$(thrift_LIBDIR)
test2_LDADD = ../../lib/cpp/libnicejson.a $(thrift_LIBS) $(BOOST_FILESYSTEM_LDADD) $(BOOST_SYSTEM_LDADD)
test2_CXXFLAGS = -I../../lib/cpp $(thrift_CFLAGS) $(AM_CXXFLAGS)

TESTS= test1 test2

THRIFT=$(thrift_EXEC_PREFIX)/bin/thrift
PLUGIN_THRIFT=$(THRIFT_SRC_ROOT)/compiler/cpp/src/thrift/plugin/plugin.thrift

$(GENCPP0_test0):
	$(THRIFT) --gen cpp -r test0.thrift

$(GENCPP_test):
	$(THRIFT) --gen cpp -r test.thrift

$(GENCPP_TYPELIB_test):
	PATH=../../plugins:${PATH} $(THRIFT) -r -gen typelib:cpp,typelib test.thrift

$(GENCPP_TYPELIB_test0):
	PATH=../../plugins:${PATH} $(THRIFT) -r -gen typelib:cpp,typelib test0.thrift

$(GENCPP_TYPELIB_plugin):
	PATH=../../plugins:${PATH} $(THRIFT) -r -gen typelib:cpp,typelib $(PLUGIN_THRIFT)

gen-json: $(GENJSON0_test0) $(GENJSON_test) $(GENJSON_plugin)

$(GENJSON0_test0):
	$(THRIFT) --gen json -r test0.thrift

$(GENJSON_test):
	$(THRIFT) --gen json -r test.thrift

$(GENJSON_plugin):
	$(THRIFT) -r -gen json $(PLUGIN_THRIFT)
