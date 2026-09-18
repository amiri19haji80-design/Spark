cd ~/work/core/pipelines/alpha/crm/crm_plus/modules && for f in meeting_attachment_bronze meeting_sub_type_bronze employee_bronze mkt_client_bronze event_attendee_bronze event_budget_bronze coverage_bronze client_hierarchy_bronze opty_flowstr_bronze opty_servicetype_info_bronze opty_participants_info_bronze opty_accesslist_info_bronze opty_failure_reason_gm_bronze actions_todos_bronze actions_todos_asgn_bronze; do grep -q "\b$f\b" crm_plus_app.py && echo "OK   $f" || echo "MISS $f"; done



grep -nE "^(def |[a-z_]+ *= *partial\()" ~/work/core/pipelines/alpha/crm/crm_plus/modules/crm_plus_app.py
