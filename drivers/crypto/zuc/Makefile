# SPDX-License-Identifier: BSD-3-Clause
# Copyright(c) 2016-2019 Intel Corporation

include $(RTE_SDK)/mk/rte.vars.mk

# library name
LIB = librte_pmd_zuc.a

# build flags
CFLAGS += -O3
CFLAGS += $(WERROR_FLAGS)
CFLAGS += -DALLOW_EXPERIMENTAL_API

# versioning export map
EXPORT_MAP := rte_pmd_zuc_version.map

# external library dependencies
LDLIBS += -lIPSec_MB
LDLIBS += -lrte_eal -lrte_mbuf -lrte_mempool -lrte_ring
LDLIBS += -lrte_cryptodev
LDLIBS += -lrte_bus_vdev

IMB_HDR = $(shell echo '\#include <intel-ipsec-mb.h>' | \
	$(CC) -E $(EXTRA_CFLAGS) - | grep 'intel-ipsec-mb.h' | \
	head -n1 | cut -d'"' -f2)

# Detect library version
IMB_VERSION = $(shell grep -e "IMB_VERSION_STR" $(IMB_HDR) | cut -d'"' -f2)
IMB_VERSION_NUM = $(shell grep -e "IMB_VERSION_NUM" $(IMB_HDR) | cut -d' ' -f3)

ifeq ($(IMB_VERSION),)
$(error "IPSec_MB version >= 0.53 is required")
endif

ifeq ($(shell expr $(IMB_VERSION_NUM) \< 0x3400), 1)
$(error "IPSec_MB version >= 0.53 is required")
endif
# library source files
SRCS-$(CONFIG_RTE_LIBRTE_PMD_ZUC) += rte_zuc_pmd.c
SRCS-$(CONFIG_RTE_LIBRTE_PMD_ZUC) += rte_zuc_pmd_ops.c

include $(RTE_SDK)/mk/rte.lib.mk
