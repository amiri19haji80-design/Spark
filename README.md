#!/bin/bash
cd ~/work/core/pipelines/alpha/crm/crm_plus || exit 1
TPL=crm_plus_contact_kdm_audit_bronze/crm_plus_contact_kdm_audit_bronze.yaml

gen() {
  mkdir -p "$1"
  sed -e "s|crm_plus_contact_kdm_audit_bronze|$1|" \
      -e "s|function: contact_kdm_audit_bronze|function: $2|" \
      "$TPL" > "$1/$1.yaml"
}

gen crm_plus_meeting_attachment_bronze meeting_attachment_bronze
gen crm_plus_meeting_sub_type_bronze meeting_sub_type_bronze
gen crm_plus_emp_info_bronze employee_bronze
gen crm_plus_client_info_bronze mkt_client_bronze
gen crm_plus_event_attendee_bronze event_attendee_bronze
gen crm_plus_event_cc_budget_bronze event_budget_bronze
gen crm_plus_coverage_info_stock_bronze coverage_bronze
gen crm_plus_client_hierarchy_info_bronze client_hierarchy_bronze
gen crm_plus_opty_flowstr opty_flowstr_bronze
gen crm_plus_opty_servicetype_info opty_servicetype_info_bronze
gen crm_plus_opty_participants_info opty_participants_info_bronze
gen crm_plus_opty_accesslist_info opty_accesslist_info_bronze
gen crm_plus_opty_failure_reason_gm opty_failure_reason_gm_bronze
gen crm_plus_actions_todos actions_todos_bronze
gen crm_plus_actions_todos_asgn actions_todos_asgn_bronze

ls -d */ | wc -l
grep -h "name:\|function:" crm_plus_emp_info_bronze/*.yaml
