# Job Search Application

## 1.0 Project Organization Tree

```
root/
├── properties/ (Data Inputs)
│   ├── experiment_metadata/
│   │   ├── experiment_id: uuid
│   │   ├── timestamp: datetime
│   │   └── hypothesis: string (e.g., "Adding Azure keywords bypasses the 48-hour auto-reject")
│   ├── independent_variables/ (The Resume)
│   │   ├── resume_version: string (e.g., "v1_data_focus", "v2_dev_focus")
│   │   ├── keyword_set: list (e.g., ["Azure", "ETL", "Databricks"])
│   │   └── email_alias: string (for shadow testing)
│   ├── control_variables/ (The Job)
│   │   ├── company_name: string
│   │   ├── role_seniority: enum (Junior, Mid, Senior)
│   │   ├── industry: string (SaaS, Manufacturing, etc.)
│   │   └── ats_platform: string (Greenhouse, Workday, Lever)
│   └── dependent_variables/ (The Outcome)
│       ├── application_status: enum (Submitted, Screened, Interview, Declined)
│       ├── response_time_hours: integer
│       └── feedback_type: enum (Auto-Reject, Human-Template, Personalized)
│
└── methods/ (System Actions)
    ├── ingestion_phase/
    │   ├── parse_job_description() -> extract_top_5_keywords
    │   ├── calculate_keyword_delta(resume_keywords, job_keywords)
    │   └── submit_application(target_url, resume_v_id)
    ├── probing_phase/
    │   ├── trigger_shadow_probe() (Submit 'over-qualified' resume to check ATS sensitivity)
    │   ├── track_link_telemetry() (Monitor GitHub/Portfolio click rates via bit.ly)
    │   └── simulate_human_follow_up(days_elapsed)
    ├── evaluation_phase/
    │   ├── analyze_rejection_patterns() (Correlation between keywords and response time)
    │   ├── validate_skill_match() (Determine if 'Cloud Awareness' vs 'Cloud Expertise' impacts outcome)
    │   └── generate_learning_backlog() (Identify recurring missing credentials)
    └── iteration_phase/
        ├── update_resume_schema() (Refining descriptors based on successful probes)
        └── pivot_target_market() (If 'Data Analyst' yields 0% success, try 'Junior Data Engineer')
```
