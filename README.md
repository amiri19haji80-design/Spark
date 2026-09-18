cd ~/work/core/pipelines/alpha/crm/crm_plus/modules
for f in meeting_attachment_bronze meeting_sub_type_bronze employee_bronze \
  mkt_client_bronze event_attendee_bronze event_budget_bronze coverage_bronze \
  client_hierarchy_bronze opty_flowstr_bronze opty_servicetype_info_bronze \
  opty_participants_info_bronze opty_accesslist_info_bronze \
  opty_failure_reason_gm_bronze actions_todos_bronze actions_todos_asgn_bronze; do
  grep -q "\b$f\b" crm_plus_app.py && echo "OK   $f" || echo "MISS $f"
done






cd ~/work/core/pipelines/alpha/crm/crm_plus
TPL=crm_plus_meeting_bronze/crm_plus_meeting_bronze.yaml
while read -r t f; do
  mkdir -p "$t"
  sed -e "s|crm_plus_meeting_bronze|$t|g" -e "s|function: meeting_bronze|function: $f|" "$TPL" > "$t/tasks.yaml"
done <<'EOF'
crm_plus_meeting_attachment_bronze meeting_attachment_bronze
crm_plus_meeting_sub_type_bronze meeting_sub_type_bronze
crm_plus_emp_info_bronze employee_bronze
crm_plus_client_info_bronze mkt_client_bronze
crm_plus_event_attendee_bronze event_attendee_bronze
crm_plus_event_cc_budget_bronze event_budget_bronze
crm_plus_coverage_info_stock_bronze coverage_bronze
crm_plus_client_hierarchy_info_bronze client_hierarchy_bronze
crm_plus_opty_flowstr opty_flowstr_bronze
crm_plus_opty_servicetype_info opty_servicetype_info_bronze
crm_plus_opty_participants_info opty_participants_info_bronze
crm_plus_opty_accesslist_info opty_accesslist_info_bronze
crm_plus_opty_failure_reason_gm opty_failure_reason_gm_bronze
crm_plus_actions_todos actions_todos_bronze
crm_plus_actions_todos_asgn actions_todos_asgn_bronze
EOF

diff "$TPL" crm_plus_emp_info_bronze/tasks.yaml
