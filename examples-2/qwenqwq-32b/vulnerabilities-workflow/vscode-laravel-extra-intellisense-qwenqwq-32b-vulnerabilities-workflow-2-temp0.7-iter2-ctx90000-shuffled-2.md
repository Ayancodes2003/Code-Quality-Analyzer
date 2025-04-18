- vulnerability name: Arbitrary Code Execution via phpCommand Configuration
  description:
  1. The extension uses the user-configurable `phpCommand` setting to execute PHP code.
  2. The default is `php -r "{code}"`, where `{code}` is PHP code generated by the extension.
  3. An attacker can manipulate this setting to inject malicious PHP execution via crafted commands:
     - Set `phpCommand` to `"php -r 'exec(\"malicious_code\");' && {code}"`
     - The malicious PHP executes before the intended code, allowing arbitrary system commands.
     - Docker configurations allow injection via placeholders (e.g., `YOUR_SERVICE_NAME`).
  4. The extension executes unvalidated commands without input sanitization.

  impact:
  Attackers gain full control over the user’s system by executing arbitrary PHP or shell commands. This includes access to the Laravel application’s environment, database, and files.

  vulnerability rank: critical
  currently implemented mitigations: None. The setting is accepted as-is from user configuration.
  missing mitigations:
  - Input validation to ensure `phpCommand` syntax is safe (e.g., restrict to trusted PHP paths).
  - Sanitization to prevent shell metacharacters in the command template.
  - Whitelisting allowed commands or enforcing a secure default structure.

  preconditions:
  - User must configure `phpCommand` with malicious content.
  - VS Code extension must be active in a Laravel project.

  source code analysis:
  In `Helpers.ts` line 199:
  ```typescript
  let commandTemplate = vscode.workspace.getConfiguration("...").get<string>('phpCommand') ?? "...";
  let command = commandTemplate.replace("{code}", code);
  ```
  The `phpCommand` is interpolated directly with no validation. Attackers could set it to `"php -r '...malicious code...' && {code}"`, which executes immediately.

  In Docker config examples:
  ```json
  "LaravelExtraIntellisense.phpCommand": "docker exec -w ... php -r \"{code}\""
  ```
  The `YOUR_SERVICE_NAME` placeholder can be manipulated to inject commands (e.g., `; rm -rf /`).

  security test case:
  1. Install the extension and open a Laravel project.
  2. Configure `phpCommand` to:
     ```json
     "LaravelExtraIntellisense.phpCommand": "php -r 'file_put_contents(\"/tmp/attacker.txt\", \"compromised\");' && {code}"
     ```
  3. Trigger any PHP execution via the extension (e.g., view autocomplete).
  4. Verify `/tmp/attacker.txt` is created.
