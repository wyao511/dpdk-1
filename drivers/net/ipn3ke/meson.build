# SPDX-License-Identifier: BSD-3-Clause
# Copyright(c) 2019 Intel Corporation

#
# Add the experimenatal APIs called from this PMD
#  rte_eth_switch_domain_alloc()
#  rte_eth_dev_create()
#  rte_eth_dev_destroy()
#  rte_eth_switch_domain_free()
#

dep = dependency('libfdt', required: false)
if not dep.found()
	dep = cc.find_library('libfdt', required: false)
endif
if not dep.found()
	build = false
	reason = 'missing dependency, "libfdt"'
	subdir_done()
endif

allow_experimental_apis = true

includes += include_directories('../../raw/ifpga')

sources += files('ipn3ke_ethdev.c',
	'ipn3ke_representor.c',
	'ipn3ke_tm.c',
	'ipn3ke_flow.c')
deps += ['bus_ifpga', 'ethdev', 'sched']
