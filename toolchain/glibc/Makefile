PATH_PREFIX := .
VARIANT:=final
HOST_BUILD_PARALLEL:=1

include ./common.mk

define Host/Compile
	+$(MAKE) -C $(CUR_BUILD_DIR) \
		PARALLELMFLAGS="$(HOST_JOBS)" \
		BUILD_CFLAGS="$(HOST_CFLAGS)" \
		default-rpath="/opt/lib:/opt/usr/lib" \
		all
endef

define Host/Install
	$(call Host/SetToolchainInfo)
	$(MAKE) -C $(CUR_BUILD_DIR) \
		BUILD_CFLAGS="$(HOST_CFLAGS)" \
		install_root="$(TOOLCHAIN_DIR)" \
		install
	( cd $(TOOLCHAIN_DIR) ; \
		for d in lib usr/lib ; do \
		  for f in libc.so libpthread.so libgcc_s.so libm.so ; do \
		    if [ -f $$$$d/$$$$f -a ! -L $$$$d/$$$$f ] ; then \
		      $(SED) 's,/usr/lib/,,g;s,/lib/,,g' $$$$d/$$$$f ; \
		    fi \
		  done \
		done \
	)
# use cross-rpcgen instead of native rpcgen as we are CROSS compiling!!!
	$(CP) $(CUR_BUILD_DIR)/sunrpc/cross-rpcgen $(TOOLCHAIN_DIR)/bin
	$(MV) -f $(TOOLCHAIN_DIR)/bin/rpcgen $(TOOLCHAIN_DIR)/bin/native-rpcgen
	$(LN) -sf $(TOOLCHAIN_DIR)/bin/cross-rpcgen $(TOOLCHAIN_DIR)/bin/rpcgen
endef

$(eval $(call HostBuild))
