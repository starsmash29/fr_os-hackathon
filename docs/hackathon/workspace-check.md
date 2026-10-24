# Workspace check

A smoke check of this workspace (hackathon issue #2). It records what the test
suites do here; it fixes nothing and changes no other file.

## Environment

- Python **3.12.3** (the target is 3.11; 3.12 is accepted for this check).
- Installed in a virtual environment with `pip install -e '.[webui,dev]'`.
  The install succeeded.
- Ran unprivileged, as uid 1000.
- Missing binaries on this machine: `nft`, `clang`, `shellcheck`, `dmidecode`,
  `conntrack`. Present: `ip`, `systemd-analyze`.

## Results

Run as AGENTS.md says, in two separate invocations.

`python3 -m pytest tests --ignore=tests/webui -q`

```
91 failed, 2318 passed, 248 skipped, 2 warnings in 429.91s (0:07:09)
```

`python3 -m pytest tests/webui -q`

```
475 passed, 1 warning in 285.50s (0:04:45)
```

The webUI suite is green. The 248 skips in the first suite are the root-only
and kernel tests skipping themselves, which is expected.

## Failing tests

All 91 are in the first suite. 72 of them are in `tests/test_helper.py`: the
apply-helper refuses each command from uid 1000 (`firewall-helper: refused
'apply' from pid … uid 1000`), so the tests fail rather than skip themselves.
The rest need a binary that is not installed here, mostly `nft`. Not
investigated further and not fixed — issue #2 asks only that they be recorded.

- `tests/test_appid.py::test_provision_merges_short_blocked_app_names_into_xdp_blocklist`
- `tests/test_helper.py::test_a_failed_apply_answers_with_what_was_rolled_back`
- `tests/test_helper.py::test_a_host_on_the_wan_is_never_looked_up_by_mac`
- `tests/test_helper.py::test_a_large_conntrack_sample_reaches_the_ids`
- `tests/test_helper.py::test_a_sign_in_over_ipv6_admits_the_whole_device`
- `tests/test_helper.py::test_a_wireguard_client_is_signed_in_at_both_its_tunnel_addresses`
- `tests/test_helper.py::test_an_address_that_isn_t_on_the_router_leaves_config_yaml_alone`
- `tests/test_helper.py::test_an_apply_that_would_move_the_webui_is_refused`
- `tests/test_helper.py::test_an_apply_through_the_helper_records_the_config_it_applied`
- `tests/test_helper.py::test_an_apply_without_confirm_is_not_held`
- `tests/test_helper.py::test_apply_dry_run`
- `tests/test_helper.py::test_apply_real_then_rollback_roundtrip`
- `tests/test_helper.py::test_authorize_ztna_fails_for_invalid_ip`
- `tests/test_helper.py::test_authorize_ztna_fails_for_unknown_user`
- `tests/test_helper.py::test_authorize_ztna_fails_when_gate_disabled`
- `tests/test_helper.py::test_authorize_ztna_success_then_status_round_trip`
- `tests/test_helper.py::test_ban_ip_defaults_to_one_hour`
- `tests/test_helper.py::test_ban_ip_jails_an_ipv6_host_by_its_mac_or_its_address`
- `tests/test_helper.py::test_ban_ip_rejects_invalid_address`
- `tests/test_helper.py::test_ban_ip_rejects_missing_ip`
- `tests/test_helper.py::test_ban_ip_rejects_non_integer_duration`
- `tests/test_helper.py::test_ban_ip_success_calls_nft_add_element`
- `tests/test_helper.py::test_bruteforce_status_empty_by_default`
- `tests/test_helper.py::test_bruteforce_status_reflects_kernel_state_after_ban`
- `tests/test_helper.py::test_conntrack_sample_empty_by_default`
- `tests/test_helper.py::test_conntrack_sample_relays_flows`
- `tests/test_helper.py::test_dhcp_leases_empty_without_lease_file`
- `tests/test_helper.py::test_dhcp_leases_relays_active_leases`
- `tests/test_helper.py::test_hw_ram_info_empty_when_dmidecode_unavailable`
- `tests/test_helper.py::test_hw_ram_info_relays_parsed_modules`
- `tests/test_helper.py::test_ids_quarantine_status_empty_when_nothing_quarantined`
- `tests/test_helper.py::test_ids_quarantine_status_lists_the_macs_held`
- `tests/test_helper.py::test_ids_quarantine_status_reflects_kernel_state_after_quarantine`
- `tests/test_helper.py::test_iot_sync_isolation_drops_trusted_macs`
- `tests/test_helper.py::test_iot_sync_isolation_refused_when_disabled`
- `tests/test_helper.py::test_iot_sync_isolation_rejects_malformed_input`
- `tests/test_helper.py::test_ipv6_status_relays_what_the_kernel_says`
- `tests/test_helper.py::test_ipv6_status_reports_off_by_default`
- `tests/test_helper.py::test_ping`
- `tests/test_helper.py::test_quarantine_ip_caps_the_duration`
- `tests/test_helper.py::test_quarantine_ip_defaults_to_two_hours`
- `tests/test_helper.py::test_quarantine_ip_holds_a_lan_hosts_mac_for_ipv6[eth0-False]`
- `tests/test_helper.py::test_quarantine_ip_holds_a_lan_hosts_mac_for_ipv6[eth1-True]`
- `tests/test_helper.py::test_quarantine_ip_holds_a_lan_hosts_mac_for_ipv6[eth2-True]`
- `tests/test_helper.py::test_quarantine_ip_holds_an_ipv6_host_by_its_mac`
- `tests/test_helper.py::test_quarantine_ip_refuses_non_host_addresses[0.0.0.0]`
- `tests/test_helper.py::test_quarantine_ip_refuses_non_host_addresses[127.0.0.1]`
- `tests/test_helper.py::test_quarantine_ip_refuses_non_host_addresses[169.254.1.1]`
- `tests/test_helper.py::test_quarantine_ip_refuses_non_host_addresses[224.0.0.251]`
- `tests/test_helper.py::test_quarantine_ip_refuses_non_host_addresses[255.255.255.255]`
- `tests/test_helper.py::test_quarantine_ip_refuses_the_routers_own_address`
- `tests/test_helper.py::test_quarantine_ip_rejects_invalid_address`
- `tests/test_helper.py::test_quarantine_ip_rejects_missing_ip`
- `tests/test_helper.py::test_quarantine_ip_rejects_non_integer_duration`
- `tests/test_helper.py::test_quarantine_ip_success_calls_nft_add_element`
- `tests/test_helper.py::test_refresh_adblock_fails_with_no_source_urls`
- `tests/test_helper.py::test_refresh_adblock_success`
- `tests/test_helper.py::test_refresh_adblock_writes_categories_and_reports_counts`
- `tests/test_helper.py::test_rollback_without_prior_apply_reports_error`
- `tests/test_helper.py::test_source_device_names_an_ipv6_lan_hosts_mac`
- `tests/test_helper.py::test_the_admin_s_action_changes_nothing_else`
- `tests/test_helper.py::test_the_admin_s_action_moves_the_webui_alone_and_holds_it`
- `tests/test_helper.py::test_the_conntrack_sample_labels_ipv6_lan_sources_with_their_mac`
- `tests/test_helper.py::test_the_helper_confirms_by_id_only`
- `tests/test_helper.py::test_the_helper_goes_back_on_request`
- `tests/test_helper.py::test_the_helper_holds_an_apply_from_the_webui_and_refuses_another`
- `tests/test_helper.py::test_unknown_command_returns_error`
- `tests/test_helper.py::test_ztna_binds_a_wireguard_client_to_its_tunnel_address`
- `tests/test_helper.py::test_ztna_binds_the_device_not_the_address`
- `tests/test_helper.py::test_ztna_refuses_a_client_the_router_is_not_attached_to`
- `tests/test_helper.py::test_ztna_sessions_status_empty_when_gate_disabled`
- `tests/test_helper.py::test_ztna_sessions_status_reflects_kernel_state_after_authorization`
- `tests/test_helper.py::test_ztna_status_reports_unauthorized_for_unknown_ip`
- `tests/test_installer.py::test_fr_first_boot_service_is_valid`
- `tests/test_integrity_signed.py::test_the_offline_check_passes_a_clean_medium`
- `tests/test_management.py::test_the_webui_does_not_listen_on_every_address`
- `tests/test_management.py::test_the_webui_listens_where_the_applied_config_says`
- `tests/test_provision.py::test_an_unreadable_set_stops_the_apply_before_the_reload`
- `tests/test_provision.py::test_apply_all_applies_addresses_and_dhcp_together`
- `tests/test_provision.py::test_apply_all_does_not_touch_xdp_blocklist_when_critical_limit_is_zero`
- `tests/test_provision.py::test_apply_all_dry_run_touches_nothing`
- `tests/test_provision.py::test_apply_all_merges_adblock_critical_domains_into_xdp_blocklist_without_persisting`
- `tests/test_provision.py::test_runtime_sets_come_back_in_the_same_ruleset`
- `tests/test_provision.py::test_ztna_and_iot_sets_are_read_only_while_on`
- `tests/test_system_units.py::test_new_daemon_units_are_valid[fr-appid.service]`
- `tests/test_system_units.py::test_new_daemon_units_are_valid[fr-tls-fp.service]`
- `tests/test_transaction.py::test_the_preflight_refuses_before_anything_changes[the XDP SNI filter-<lambda>]`
- `tests/test_update_systemd_units.py::test_unit_is_valid[fr-update-helper.service]`
- `tests/test_webui_tls.py::test_the_real_webui_refuses_tls_below_1_2`
- `tests/test_webui_tls.py::test_with_pqc_the_real_webui_is_tls_1_3_only`
- `tests/test_xdp_systemd_unit.py::test_unit_is_valid`

