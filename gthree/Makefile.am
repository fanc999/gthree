NULL =
CLEANFILES =
MAINTAINERCLEANFILES =
EXTRA_DIST =
BUILT_SOURCES =
lib_LTLIBRARIES =

AM_CPPFLAGS =					\
	-I$(top_srcdir)				\
	-I$(top_builddir)			\
	-DLIBEXECDIR=\"$(libexecdir)\"		\
	-DBINDIR=\"$(bindir)\"			\
	-DLIBDIR=\"$(libdir)\"			\
	-DGTHREE_COMPILATION			\
	$(NULL)

lib_LTLIBRARIES += libgthree-1.la

libgthree_1_ladir = $(includedir)/gthree

gthree_public_h_sources = \
	gthree.h \
	gthreearea.h \
	gthreebasicmaterial.h \
	gthreecamera.h \
	gthreeperspectivecamera.h \
	gthreeambientlight.h \
	gthreedirectionallight.h \
	gthreepointlight.h \
	gthreelight.h \
	gthreeenums.h \
	gthreegeometry.h \
	gthreematerial.h \
	gthreemesh.h \
	gthreemultimaterial.h \
	gthreelambertmaterial.h \
	gthreephongmaterial.h \
	gthreenormalmaterial.h \
	gthreedepthmaterial.h \
	gthreeobject.h \
	gthreerenderer.h \
	gthreescene.h \
	gthreetexture.h \
	gthreecubetexture.h \
	gthreetypes.h \
	gthreeprogram.h			\
	gthreeshader.h \
	gthreeshadermaterial.h \
	gthreeuniforms.h \
	gthreeloader.h			\
	$(NULL)

gthree_private_h_sources =		\
	gthreebufferprivate.h		\
	gthreegeometrygroupprivate.h	\
	gthreeobjectprivate.h		\
	gthreeprivate.h			\
	$(NULL)

gthree_built_public_sources =			\
	gthreetypebuiltins.h			\
	$(NULL)

gthree_built_private_headers =			\
	gthree-resources.h			\
	gthreemarshalers.h			\
	$(NULL)

stamp_files =					\
	stamp-gthreemarshalers.h		\
	stamp-gthreetypebuiltins.h		\
	$(NULL)

gthree_built_sources =				\
	gthree-resources.c			\
	gthreetypebuiltins.c			\
	${gthree_built_private_headers}		\
	${gthree_built_public_sources}		\
	$(NULL)

gthree_extra_sources =				\
	gthreemarshalers.list			\
	$(NULL)

gthree_c_sources = \
	gthreearea.c \
	gthreebuffer.c \
	gthreecamera.c \
	gthreeperspectivecamera.c \
	gthreeambientlight.c \
	gthreedirectionallight.c \
	gthreepointlight.c \
	gthreelight.c \
	gthreegeometry-utils.c \
	gthreegeometry.c \
	gthreegeometrygroup.c \
	gthreematerial.c \
	gthreeshadermaterial.c \
	gthreebasicmaterial.c \
	gthreemultimaterial.c \
	gthreelambertmaterial.c \
	gthreephongmaterial.c \
	gthreenormalmaterial.c \
	gthreedepthmaterial.c \
	gthreemesh.c \
	gthreeobject.c \
	gthreeprogram.c \
	gthreeuniforms.c \
	gthreerenderer.c \
	gthreescene.c \
	gthreeshader.c \
	gthreetexture.c \
	gthreecubetexture.c \
	gthreeloader.c \
	gthreemarshalers.c \
	$(NULL)

MAINTAINERCLEANFILES += \
	$(gthree_built_sources)	\
	$(stamp_files) \
	$(NULL)

gthreeincludedir = $(includedir)/gthree-1.0/gthree
gthreeinclude_HEADERS = $(gthree_public_h_sources)

EXTRA_DIST += $(gthree_private_h_sources) $(gthree_built_sources) $(gthree_extra_sources)

BUILT_SOURCES += \
	$(gthree_built_sources) \
	$(NULL)

gthreemarshalers.h: stamp-gthreemarshalers.h
	@true
stamp-gthreemarshalers.h: gthreemarshalers.list
	$(AM_V_GEN) $(GLIB_GENMARSHAL) --prefix=_gthree_marshal $(srcdir)/gthreemarshalers.list --header --valist-marshallers >> xgen-gmlh \
	&& (cmp -s xgen-gmlh gthreemarshalers.h || cp xgen-gmlh gthreemarshalers.h) \
	&& rm -f xgen-gmlh \
	&& echo timestamp > $(@F)
gthreemarshalers.c: gthreemarshalers.list
	$(AM_V_GEN) (echo "#include \"gthreemarshalers.h\""; \
	 $(GLIB_GENMARSHAL) --prefix=_gthree_marshal $(srcdir)/gthreemarshalers.list --body  --valist-marshallers) >> xgen-gmlc \
	&& cp xgen-gmlc gthreemarshalers.c \
	&& rm -f xgen-gmlc

gthreetypebuiltins.h: stamp-gthreetypebuiltins.h
	@true
stamp-gthreetypebuiltins.h: $(gthree_public_h_sources) gthreetypebuiltins.h.template
	$(AM_V_GEN) ( cd $(srcdir) && $(GLIB_MKENUMS) --template gthreetypebuiltins.h.template \
		$(gthree_public_h_sources) ) > xgen-gtbh \
	&& (cmp -s xgen-gtbh gthreetypebuiltins.h || cp xgen-gtbh gthreetypebuiltins.h ) \
	&& rm -f xgen-gtbh \
	&& echo timestamp > $(@F)
gthreetypebuiltins.c: $(gthree_public_h_sources) gthreetypebuiltins.c.template
	$(AM_V_GEN) ( cd $(srcdir) && $(GLIB_MKENUMS) --template gthreetypebuiltins.c.template \
		$(gthree_public_h_sources) ) > xgen-gtbc \
	&& cp xgen-gtbc gthreetypebuiltins.c  \
	&& rm -f xgen-gtbc

resource_files = $(shell glib-compile-resources --sourcedir=$(srcdir) --generate-dependencies $(srcdir)/gthree.gresource.xml)

gthree-resources.c: gthree.gresource.xml $(resource_files)
	$(AM_V_GEN) glib-compile-resources --target=$@ --sourcedir=$(srcdir) --generate-source --c-name gthree $(srcdir)/gthree.gresource.xml

gthree-resources.h: gthree.gresource.xml $(resource_files)
	$(AM_V_GEN) glib-compile-resources --target=$@ --sourcedir=$(srcdir) --generate-header --c-name gthree $(srcdir)/gthree.gresource.xml


libgthree_1_la_SOURCES = $(gthree_built_sources) $(gthree_c_sources)
libgthree_1_la_CFLAGS = $(GTHREE_CFLAGS)
libgthree_1_la_LIBADD =	$(GTHREE_LIBS) $(LIBM)

EXTRA_DIST += \
	gthreetypebuiltins.c.template \
	gthreetypebuiltins.h.template \
	$(NULL)

-include $(INTROSPECTION_MAKEFILE)

if HAVE_INTROSPECTION

INTROSPECTION_GIRS = Gthree-1.0.gir

introspection_source_h = $(gthree_public_h_sources)
introspection_source_c = $(gthree_c_sources)

Gthree-1.0.gir: libgthree-1.la Makefile

Gthree_1_0_gir_VERSION = 1.0
Gthree_1_0_gir_LIBS = libgthree-1.la
Gthree_1_0_gir_SCANNERFLAGS = \
	--warn-all \
	--c-include="gthree.h" \
	--pkg-export gthree-1.0

Gthree_1_0_gir_PACKAGES = gtk+-3.0 graphene-gobject-1.0
Gthree_1_0_gir_INCLUDES = Gtk-3.0 Graphene-1.0
Gthree_1_0_gir_CFLAGS = -DGTHREE_COMPILATION -I$(top_srcdir) -I$(top_builddir)
Gthree_1_0_gir_FILES = $(introspection_source_h) $(introspection_source_c)

girdir = $(datadir)/gir-1.0
nodist_gir_DATA = $(INTROSPECTION_GIRS)
CLEANFILES += $(nodist_gir_DATA)

typelibdir = $(libdir)/girepository-1.0
nodist_typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)
CLEANFILES += $(nodist_typelib_DATA)

endif # HAVE_INTROSPECTION
