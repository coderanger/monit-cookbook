# Monit Cookbook
[![License](https://img.shields.io/badge/license-Apache_2-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

[Application cookbook][0] which installs and configures the [monit][1] process monitoring daemon. Currently it defaults to ubuntu.

## Usage
### Supports
- Ubuntu
- RHEL

### Dependencies
| Name | Description |
|------|-------------|
| [poise][2] | [Library cookbook][4] built to aide in writing reusable cookbooks. |
| [poise-service][3] | [Library cookbook][4] built to abstract service management. |

### Attributes
The basic attributes to get the services up/running/monitored are available in the [library][5]. Anything additional please create a PR.

### Resources/Providers

#### monit_config
Example below:

```ruby
monit_config 'your_dope_service' do
  check  'process'
  with   'pidfile "/var/run/your_dope_service"
  start_program   "/bin/bash -c '/bin/sleep 5; /etc/init.d/your_dope_service start'"
  stop_program    '/etc/init.d/your_dope_service stop'
  notifies :restart, "service[monit_#{new_resource.instance_name}]", :immediately
end
```

License & Authors
-----------------
- Author:: Anthony Caiafa (<acaiafa1@bloomberg.net>)

```text
Copyright 2015 Bloomberg Finance L.P.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

[0]: http://blog.vialstudios.com/the-environment-cookbook-pattern#theapplicationcookbook
[1]: https://mmonit.com/monit/
[2]: https://github.com/poise/poise
[3]: https://github.com/poise/poise-service
[4]: http://blog.vialstudios.com/the-environment-cookbook-pattern#thelibrarycookbook
[5]: libraries/monit_config.rb
