## Grep for Dangerous Calls
grep -rn --include="*.py" -E "os\.system|subprocess|eval\(|exec\(|pickle\.loads|render_template_string|cursor\.execute|send_file|open\(" .

## Grep for Secrets and Config
Two more passes pay off immediately. The first hunts hardcoded secrets by variable name:
grep -rnE "(SECRET|KEY|TOKEN|PASSWORD|API_KEY)\s*=\s*['\"]" --include="*.py" .

The second hunts configuration antipatterns: debug left on, TLS verification disabled.
grep -rnE "DEBUG\s*=\s*True|TESTING\s*=\s*True|verify\s*=\s*False" .

A useful one-off is the AWS access key ID pattern, which has a fixed shape we can match exactly.
grep -rE "AKIA[0-9A-Z]{16}" .

## Semgrep for Rule-Based Triage
$ pip install semgrep        # already installed on the room's machine
$ semgrep --config p/owasp-top-ten . 