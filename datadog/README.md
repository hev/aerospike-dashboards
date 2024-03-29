## Overview

Some temporary instructions to correct the instructions provided on the 
official [Aerospike Datadog Integration](https://github.com/DataDog/integrations-core/tree/master/aerospike).

## Setup
1. Edit the `/opt/datadog-agent/etc/datadog.yaml' file to include the prometheus/openmetrics integration by
setting the following.
```
prometheus:

  ## @param enabled - boolean - optional - default: false
  ## Enables the prometheus config provider
  #
  enabled: true

  ## @param service_endpoints - boolean - optional - default: false
  ## Enables Service Endpoints checks in the prometheus config provider
  #
  service_endpoints: true
```

2. Instead of editing 'aerospike.d/conf.yaml' file, edit the `openmetrics.d/conf.yaml' file.
3. Add details about the scrape endpoint
```
instances:

  -
    ## @param openmetrics_endpoint - string - optional
    ## The URL exposing metrics in the OpenMetrics format.
    #
    openmetrics_endpoint: http://localhost:9145/metrics
```
4. Add an allow list of metrics to include, or specificy all through a *. THis list here includes new set level config exposed in Aerospike 6.3.


reg-ex approach (this didn't work for me)

```
 metrics:
      - *
```

allow list approach

```
    metrics:
      - aerospike_users_conns_in_use
      - aerospike_users_read_single_record_tps
      - aerospike_users_read_scan_query_rps
      - aerospike_users_limitless_read_scan_query
      - aerospike_users_write_quota
      - aerospike_users_write_single_record_tps
      - aerospike_users_write_scan_query_rps
      - aerospike_users_limitless_write_scan_query
      - aerospike_users_write_quota
      - aerospike_sets_memory_data_bytes
      - aerospike_sets_device_data_bytes
      - aerospike_sets_stop_writes_count
      - aerospike_sets_disable_eviction
      - aerospike_sets_index_populating
      - aerospike_sets_stop_writes_size
      - aerospike_sets_enable_index
      - aerospike_sets_truncate_lut
      - aerospike_sets_tombstones
      - aerospike_sets_sindexes
      - aerospike_sets_objects
      - aerospike_sets_stop_writes_size
      - aerospike_namespace_appeals_records_exonerated
      - aerospike_namespace_appeals_records_exonerated
      - aerospike_namespace_appeals_rx_active
      - aerospike_namespace_appeals_tx_active
      - aerospike_namespace_appeals_tx_remaining
      - aerospike_namespace_available_bin_names
      - aerospike_namespace_batch_sub_delete_error
      - aerospike_namespace_batch_sub_delete_filtered_out
      - aerospike_namespace_batch_sub_delete_not_found
      - aerospike_namespace_batch_sub_delete_success
      - aerospike_namespace_batch_sub_delete_timeout
      - aerospike_namespace_batch_sub_lang_delete_success
      - aerospike_namespace_batch_sub_lang_error
      - aerospike_namespace_batch_sub_lang_read_success
      - aerospike_namespace_batch_sub_lang_write_success
      - aerospike_namespace_batch_sub_proxy_complete
      - aerospike_namespace_batch_sub_proxy_error
      - aerospike_namespace_batch_sub_proxy_timeout
      - aerospike_namespace_batch_sub_read_error
      - aerospike_namespace_batch_sub_read_filtered_out
      - aerospike_namespace_batch_sub_read_not_found
      - aerospike_namespace_batch_sub_read_success
      - aerospike_namespace_batch_sub_read_timeout
      - aerospike_namespace_batch_sub_tsvc_error
      - aerospike_namespace_batch_sub_tsvc_timeout
      - aerospike_namespace_batch_sub_udf_complete
      - aerospike_namespace_batch_sub_udf_error
      - aerospike_namespace_batch_sub_udf_filtered_out
      - aerospike_namespace_batch_sub_udf_timeout
      - aerospike_namespace_batch_sub_write_error
      - aerospike_namespace_batch_sub_write_filtered_out
      - aerospike_namespace_batch_sub_write_success
      - aerospike_namespace_batch_sub_write_timeout
      - aerospike_namespace_cache_read_pct
      - aerospike_namespace_client_delete_error
      - aerospike_namespace_client_delete_filtered_out
      - aerospike_namespace_client_delete_not_found
      - aerospike_namespace_client_delete_success
      - aerospike_namespace_client_delete_timeout
      - aerospike_namespace_client_lang_delete_success
      - aerospike_namespace_client_lang_error
      - aerospike_namespace_client_lang_read_success
      - aerospike_namespace_client_lang_write_success
      - aerospike_namespace_client_proxy_complete
      - aerospike_namespace_client_proxy_error
      - aerospike_namespace_client_proxy_timeout
      - aerospike_namespace_client_read_error
      - aerospike_namespace_client_read_filtered_out
      - aerospike_namespace_client_read_not_found
      - aerospike_namespace_client_read_success
      - aerospike_namespace_client_read_timeout
      - aerospike_namespace_client_tsvc_error
      - aerospike_namespace_client_tsvc_timeout
      - aerospike_namespace_client_udf_complete
      - aerospike_namespace_client_udf_error
      - aerospike_namespace_client_udf_filtered_out
      - aerospike_namespace_client_udf_timeout
      - aerospike_namespace_client_write_error
      - aerospike_namespace_client_write_filtered_out
      - aerospike_namespace_client_write_success
      - aerospike_namespace_client_write_timeout
      - aerospike_namespace_clock_skew_stop_writes
      - aerospike_namespace_conflict_resolve_writes
      - aerospike_namespace_current_time
      - aerospike_namespace_data_in_index
      - aerospike_namespace_dead_partitions
      - aerospike_namespace_default_ttl
      - aerospike_namespace_deleted_last_bin
      - aerospike_namespace_device_available_pct
      - aerospike_namespace_device_free_pct
      - aerospike_namespace_device_total_bytes
      - aerospike_namespace_device_used_bytes
      - aerospike_namespace_disable_cold_start_eviction
      - aerospike_namespace_disable_write_dup_res
      - aerospike_namespace_disallow_null_setname
      - aerospike_namespace_dup_res_ask
      - aerospike_namespace_dup_res_respond_no_read
      - aerospike_namespace_dup_res_respond_read
      - aerospike_namespace_effective_is_quiesced
      - aerospike_namespace_effective_prefer_uniform_balance
      - aerospike_namespace_effective_replication_factor
      - aerospike_namespace_enable_benchmarks_batch_sub
      - aerospike_namespace_enable_benchmarks_ops_sub
      - aerospike_namespace_enable_benchmarks_read
      - aerospike_namespace_enable_benchmarks_udf
      - aerospike_namespace_enable_benchmarks_udf_sub
      - aerospike_namespace_enable_benchmarks_write
      - aerospike_namespace_enable_hist_proxy
      - aerospike_namespace_evict_hist_buckets
      - aerospike_namespace_evict_tenths_pct
      - aerospike_namespace_evict_ttl
      - aerospike_namespace_evict_void_time
      - aerospike_namespace_evicted_objects
      - aerospike_namespace_expired_objects
      - aerospike_namespace_fail_client_lost_conflict
      - aerospike_namespace_fail_generation
      - aerospike_namespace_fail_key_busy
      - aerospike_namespace_fail_record_too_big
      - aerospike_namespace_fail_xdr_forbidden
      - aerospike_namespace_fail_xdr_lost_conflict
      - aerospike_namespace_from_proxy_batch_sub_delete_error
      - aerospike_namespace_from_proxy_batch_sub_delete_filtered_out
      - aerospike_namespace_from_proxy_batch_sub_delete_not_found
      - aerospike_namespace_from_proxy_batch_sub_delete_success
      - aerospike_namespace_from_proxy_batch_sub_delete_timeout
      - aerospike_namespace_from_proxy_batch_sub_lang_delete_success
      - aerospike_namespace_from_proxy_batch_sub_lang_error
      - aerospike_namespace_from_proxy_batch_sub_lang_read_success
      - aerospike_namespace_from_proxy_batch_sub_lang_write_success
      - aerospike_namespace_from_proxy_batch_sub_read_error
      - aerospike_namespace_from_proxy_batch_sub_read_filtered_out
      - aerospike_namespace_from_proxy_batch_sub_read_not_found
      - aerospike_namespace_from_proxy_batch_sub_read_success
      - aerospike_namespace_from_proxy_batch_sub_read_timeout
      - aerospike_namespace_from_proxy_batch_sub_tsvc_error
      - aerospike_namespace_from_proxy_batch_sub_tsvc_timeout
      - aerospike_namespace_from_proxy_batch_sub_udf_complete
      - aerospike_namespace_from_proxy_batch_sub_udf_error
      - aerospike_namespace_from_proxy_batch_sub_udf_filtered_out
      - aerospike_namespace_from_proxy_batch_sub_udf_timeout
      - aerospike_namespace_from_proxy_batch_sub_write_error
      - aerospike_namespace_from_proxy_batch_sub_write_filtered_out
      - aerospike_namespace_from_proxy_batch_sub_write_success
      - aerospike_namespace_from_proxy_batch_sub_write_timeout
      - aerospike_namespace_from_proxy_delete_error
      - aerospike_namespace_from_proxy_delete_filtered_out
      - aerospike_namespace_from_proxy_delete_not_found
      - aerospike_namespace_from_proxy_delete_success
      - aerospike_namespace_from_proxy_delete_timeout
      - aerospike_namespace_from_proxy_lang_delete_success
      - aerospike_namespace_from_proxy_lang_error
      - aerospike_namespace_from_proxy_lang_read_success
      - aerospike_namespace_from_proxy_lang_write_success
      - aerospike_namespace_from_proxy_read_error
      - aerospike_namespace_from_proxy_read_filtered_out
      - aerospike_namespace_from_proxy_read_not_found
      - aerospike_namespace_from_proxy_read_success
      - aerospike_namespace_from_proxy_read_timeout
      - aerospike_namespace_from_proxy_tsvc_error
      - aerospike_namespace_from_proxy_tsvc_timeout
      - aerospike_namespace_from_proxy_udf_complete
      - aerospike_namespace_from_proxy_udf_error
      - aerospike_namespace_from_proxy_udf_filtered_out
      - aerospike_namespace_from_proxy_udf_timeout
      - aerospike_namespace_from_proxy_write_error
      - aerospike_namespace_from_proxy_write_filtered_out
      - aerospike_namespace_from_proxy_write_success
      - aerospike_namespace_from_proxy_write_timeout
      - aerospike_namespace_geo2dsphere_within_earth_radius_meters
      - aerospike_namespace_geo2dsphere_within_level_mod
      - aerospike_namespace_geo2dsphere_within_max_cells
      - aerospike_namespace_geo2dsphere_within_max_level
      - aerospike_namespace_geo2dsphere_within_min_level
      - aerospike_namespace_geo2dsphere_within_strict
      - aerospike_namespace_geo_region_query_cells
      - aerospike_namespace_geo_region_query_falsepos
      - aerospike_namespace_geo_region_query_points
      - aerospike_namespace_geo_region_query_reqs
      - aerospike_namespace_high_water_disk_pct
      - aerospike_namespace_high_water_memory_pct
      - aerospike_namespace_hwm_breached
      - aerospike_namespace_ignore_migrate_fill_delay
      - aerospike_namespace_index_stage_size
      - aerospike_namespace_master_objects
      - aerospike_namespace_master_tombstones
      - aerospike_namespace_max_record_size
      - aerospike_namespace_memory_free_pct
      - aerospike_namespace_memory_size
      - aerospike_namespace_memory_used_bytes
      - aerospike_namespace_memory_used_data_bytes
      - aerospike_namespace_memory_used_index_bytes
      - aerospike_namespace_memory_used_set_index_bytes
      - aerospike_namespace_memory_used_sindex_bytes
      - aerospike_namespace_migrate_order
      - aerospike_namespace_migrate_record_receives
      - aerospike_namespace_migrate_record_retransmits
      - aerospike_namespace_migrate_records_skipped
      - aerospike_namespace_migrate_records_transmitted
      - aerospike_namespace_migrate_retransmit_ms
      - aerospike_namespace_migrate_rx_instances
      - aerospike_namespace_migrate_rx_partitions_active
      - aerospike_namespace_migrate_rx_partitions_initial
      - aerospike_namespace_migrate_rx_partitions_remaining
      - aerospike_namespace_migrate_signals_active
      - aerospike_namespace_migrate_signals_remaining
      - aerospike_namespace_migrate_sleep
      - aerospike_namespace_migrate_tx_instances
      - aerospike_namespace_migrate_tx_partitions_active
      - aerospike_namespace_migrate_tx_partitions_imbalance
      - aerospike_namespace_migrate_tx_partitions_initial
      - aerospike_namespace_migrate_tx_partitions_lead_remaining
      - aerospike_namespace_migrate_tx_partitions_remaining
      - aerospike_namespace_non_expirable_objects
      - aerospike_namespace_non_replica_objects
      - aerospike_namespace_non_replica_tombstones
      - aerospike_namespace_ns_cluster_size
      - aerospike_namespace_nsup_cycle_deleted_pct
      - aerospike_namespace_nsup_cycle_duration
      - aerospike_namespace_nsup_hist_period
      - aerospike_namespace_nsup_period
      - aerospike_namespace_nsup_threads
      - aerospike_namespace_objects
      - aerospike_namespace_ops_sub_tsvc_error
      - aerospike_namespace_ops_sub_tsvc_timeout
      - aerospike_namespace_ops_sub_write_error
      - aerospike_namespace_ops_sub_write_filtered_out
      - aerospike_namespace_ops_sub_write_success
      - aerospike_namespace_ops_sub_write_timeout
      - aerospike_namespace_partition_tree_sprigs
      - aerospike_namespace_pending_quiesce
      - aerospike_namespace_pi_query_aggr_abort
      - aerospike_namespace_pi_query_aggr_complete
      - aerospike_namespace_pi_query_aggr_error
      - aerospike_namespace_pi_query_long_basic_abort
      - aerospike_namespace_pi_query_long_basic_complete
      - aerospike_namespace_pi_query_long_basic_error
      - aerospike_namespace_pi_query_ops_bg_abort
      - aerospike_namespace_pi_query_ops_bg_complete
      - aerospike_namespace_pi_query_ops_bg_error
      - aerospike_namespace_pi_query_short_basic_complete
      - aerospike_namespace_pi_query_short_basic_error
      - aerospike_namespace_pi_query_short_basic_timeout
      - aerospike_namespace_pi_query_udf_bg_abort
      - aerospike_namespace_pi_query_udf_bg_complete
      - aerospike_namespace_pi_query_udf_bg_error
      - aerospike_namespace_prefer_uniform_balance
      - aerospike_namespace_prole_objects
      - aerospike_namespace_prole_tombstones
      - aerospike_namespace_query_proto_compression_ratio
      - aerospike_namespace_query_proto_uncompressed_pct
      - aerospike_namespace_rack_id
      - aerospike_namespace_re_repl_error
      - aerospike_namespace_re_repl_success
      - aerospike_namespace_re_repl_timeout
      - aerospike_namespace_record_proto_compression_ratio
      - aerospike_namespace_record_proto_uncompressed_pct
      - aerospike_namespace_reject_non_xdr_writes
      - aerospike_namespace_reject_xdr_writes
      - aerospike_namespace_replication_factor
      - aerospike_namespace_retransmit_all_batch_sub_dup_res
      - aerospike_namespace_retransmit_all_delete_dup_res
      - aerospike_namespace_retransmit_all_delete_repl_write
      - aerospike_namespace_retransmit_all_read_dup_res
      - aerospike_namespace_retransmit_all_udf_dup_res
      - aerospike_namespace_retransmit_all_udf_repl_write
      - aerospike_namespace_retransmit_all_write_dup_res
      - aerospike_namespace_retransmit_all_write_repl_write
      - aerospike_namespace_retransmit_ops_sub_dup_res
      - aerospike_namespace_retransmit_ops_sub_repl_write
      - aerospike_namespace_retransmit_udf_sub_dup_res
      - aerospike_namespace_retransmit_udf_sub_repl_write
      - aerospike_namespace_si_query_aggr_abort
      - aerospike_namespace_si_query_aggr_complete
      - aerospike_namespace_si_query_aggr_error
      - aerospike_namespace_si_query_long_basic_abort
      - aerospike_namespace_si_query_long_basic_complete
      - aerospike_namespace_si_query_long_basic_error
      - aerospike_namespace_si_query_ops_bg_abort
      - aerospike_namespace_si_query_ops_bg_complete
      - aerospike_namespace_si_query_ops_bg_error
      - aerospike_namespace_si_query_short_basic_complete
      - aerospike_namespace_si_query_short_basic_error
      - aerospike_namespace_si_query_short_basic_timeout
      - aerospike_namespace_si_query_udf_bg_abort
      - aerospike_namespace_si_query_udf_bg_complete
      - aerospike_namespace_si_query_udf_bg_error
      - aerospike_namespace_sindex_gc_cleaned
      - aerospike_namespace_single_bin
      - aerospike_namespace_smd_evict_void_time
      - aerospike_namespace_stop_writes
      - aerospike_namespace_stop_writes_pct
      - aerospike_namespace_stop_writes_sys_memory_pct
      - aerospike_namespace_storage_engine_cache_replica_writes
      - aerospike_namespace_storage_engine_cold_start_empty
      - aerospike_namespace_storage_engine_commit_min_size
      - aerospike_namespace_storage_engine_commit_to_device
      - aerospike_namespace_storage_engine_compression_level
      - aerospike_namespace_storage_engine_data_in_memory
      - aerospike_namespace_storage_engine_defrag_lwm_pct
      - aerospike_namespace_storage_engine_defrag_queue_min
      - aerospike_namespace_storage_engine_defrag_sleep
      - aerospike_namespace_storage_engine_defrag_startup_minimum
      - aerospike_namespace_storage_engine_direct_files
      - aerospike_namespace_storage_engine_disable_odsync
      - aerospike_namespace_storage_engine_enable_benchmarks_storage
      - aerospike_namespace_storage_engine_file_age
      - aerospike_namespace_storage_engine_file_defrag_q
      - aerospike_namespace_storage_engine_file_defrag_reads
      - aerospike_namespace_storage_engine_file_defrag_writes
      - aerospike_namespace_storage_engine_file_free_wblocks
      - aerospike_namespace_storage_engine_file_shadow_write_q
      - aerospike_namespace_storage_engine_file_used_bytes
      - aerospike_namespace_storage_engine_file_write_q
      - aerospike_namespace_storage_engine_file_writes
      - aerospike_namespace_storage_engine_filesize
      - aerospike_namespace_storage_engine_flush_max_ms
      - aerospike_namespace_storage_engine_max_used_pct
      - aerospike_namespace_storage_engine_max_write_cache
      - aerospike_namespace_storage_engine_min_avail_pct
      - aerospike_namespace_storage_engine_post_write_queue
      - aerospike_namespace_storage_engine_read_page_cache
      - aerospike_namespace_storage_engine_serialize_tomb_raider
      - aerospike_namespace_storage_engine_tomb_raider_sleep
      - aerospike_namespace_storage_engine_write_block_size
      - aerospike_namespace_strong_consistency
      - aerospike_namespace_strong_consistency_allow_expunge
      - aerospike_namespace_tomb_raider_eligible_age
      - aerospike_namespace_tomb_raider_period
      - aerospike_namespace_tombstones
      - aerospike_namespace_transaction_pending_limit
      - aerospike_namespace_truncate_lut
      - aerospike_namespace_truncate_threads
      - aerospike_namespace_udf_sub_lang_delete_success
      - aerospike_namespace_udf_sub_lang_error
      - aerospike_namespace_udf_sub_lang_read_success
      - aerospike_namespace_udf_sub_lang_write_success
      - aerospike_namespace_udf_sub_tsvc_error
      - aerospike_namespace_udf_sub_tsvc_timeout
      - aerospike_namespace_udf_sub_udf_complete
      - aerospike_namespace_udf_sub_udf_error
      - aerospike_namespace_udf_sub_udf_filtered_out
      - aerospike_namespace_udf_sub_udf_timeout
      - aerospike_namespace_unavailable_partitions
      - aerospike_namespace_unreplicated_records
      - aerospike_namespace_xdr_bin_cemeteries
      - aerospike_namespace_xdr_bin_tombstone_ttl
      - aerospike_namespace_xdr_client_delete_error
      - aerospike_namespace_xdr_client_delete_not_found
      - aerospike_namespace_xdr_client_delete_success
      - aerospike_namespace_xdr_client_delete_timeout
      - aerospike_namespace_xdr_client_write_error
      - aerospike_namespace_xdr_client_write_success
      - aerospike_namespace_xdr_client_write_timeout
      - aerospike_namespace_xdr_from_proxy_delete_error
      - aerospike_namespace_xdr_from_proxy_delete_not_found
      - aerospike_namespace_xdr_from_proxy_delete_success
      - aerospike_namespace_xdr_from_proxy_delete_timeout
      - aerospike_namespace_xdr_from_proxy_write_error
      - aerospike_namespace_xdr_from_proxy_write_success
      - aerospike_namespace_xdr_from_proxy_write_timeout
      - aerospike_namespace_xdr_tomb_raider_period
      - aerospike_namespace_xdr_tomb_raider_threads
      - aerospike_namespace_xdr_tombstones
      - aerospike_node_stats_batch_index_complete
      - aerospike_node_stats_batch_index_created_buffers
      - aerospike_node_stats_batch_index_delay
      - aerospike_node_stats_batch_index_destroyed_buffers
      - aerospike_node_stats_batch_index_error
      - aerospike_node_stats_batch_index_huge_buffers
      - aerospike_node_stats_batch_index_initiate
      - aerospike_node_stats_batch_index_proto_compression_ratio
      - aerospike_node_stats_batch_index_proto_uncompressed_pct
      - aerospike_node_stats_batch_index_timeout
      - aerospike_node_stats_batch_index_unused_buffers
      - aerospike_node_stats_client_connections
      - aerospike_node_stats_client_connections_closed
      - aerospike_node_stats_client_connections_opened
      - aerospike_node_stats_cluster_clock_skew_ms
      - aerospike_node_stats_cluster_clock_skew_stop_writes_sec
      - aerospike_node_stats_cluster_generation
      - aerospike_node_stats_cluster_integrity
      - aerospike_node_stats_cluster_is_member
      - aerospike_node_stats_cluster_max_compatibility_id
      - aerospike_node_stats_cluster_min_compatibility_id
      - aerospike_node_stats_cluster_size
      - aerospike_node_stats_demarshal_error
      - aerospike_node_stats_early_tsvc_batch_sub_error
      - aerospike_node_stats_early_tsvc_client_error
      - aerospike_node_stats_early_tsvc_from_proxy_batch_sub_error
      - aerospike_node_stats_early_tsvc_from_proxy_error
      - aerospike_node_stats_early_tsvc_ops_sub_error
      - aerospike_node_stats_early_tsvc_udf_sub_error
      - aerospike_node_stats_fabric_bulk_recv_rate
      - aerospike_node_stats_fabric_bulk_send_rate
      - aerospike_node_stats_fabric_connections
      - aerospike_node_stats_fabric_connections_closed
      - aerospike_node_stats_fabric_connections_opened
      - aerospike_node_stats_fabric_ctrl_recv_rate
      - aerospike_node_stats_fabric_ctrl_send_rate
      - aerospike_node_stats_fabric_meta_recv_rate
      - aerospike_node_stats_fabric_meta_send_rate
      - aerospike_node_stats_fabric_rw_recv_rate
      - aerospike_node_stats_fabric_rw_send_rate
      - aerospike_node_stats_failed_best_practices
      - aerospike_node_stats_heap_active_kbytes
      - aerospike_node_stats_heap_allocated_kbytes
      - aerospike_node_stats_heap_efficiency_pct
      - aerospike_node_stats_heap_mapped_kbytes
      - aerospike_node_stats_heap_site_count
      - aerospike_node_stats_heartbeat_connections
      - aerospike_node_stats_heartbeat_connections_closed
      - aerospike_node_stats_heartbeat_connections_opened
      - aerospike_node_stats_heartbeat_received_foreign
      - aerospike_node_stats_heartbeat_received_self
      - aerospike_node_stats_info_complete
      - aerospike_node_stats_info_queue
      - aerospike_node_stats_migrate_allowed
      - aerospike_node_stats_migrate_partitions_remaining
      - aerospike_node_stats_objects
      - aerospike_node_stats_process_cpu_pct
      - aerospike_node_stats_proxy_in_progress
      - aerospike_node_stats_reaped_fds
      - aerospike_node_stats_rw_in_progress
      - aerospike_node_stats_system_free_mem_pct
      - aerospike_node_stats_system_kernel_cpu_pct
      - aerospike_node_stats_system_total_cpu_pct
      - aerospike_node_stats_system_user_cpu_pct
      - aerospike_node_stats_threads_detached
      - aerospike_node_stats_threads_joinable
      - aerospike_node_stats_threads_pool_active
      - aerospike_node_stats_threads_pool_total
      - aerospike_node_stats_time_since_rebalance
      - aerospike_node_stats_tombstones
      - aerospike_node_stats_tree_gc_queue
      - aerospike_node_stats_uptime
      - aerospike_node_ticks
      - aerospike_node_up 
```