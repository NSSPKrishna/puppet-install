[![New Relic Experimental header](https://github.com/newrelic/opensource-website/raw/main/src/images/categories/Experimental.png)](https://opensource.newrelic.com/oss-category/#new-relic-experimental)
# New Relic installation using Puppet
This Puppet module installs and configures New Relic instrumentation on user-specified targets
## Installation
### Puppet Forge
**Coming soon**: `puppet module install newrelic-newrelic_installer`

### Manual
* Install puppet development kit: https://www.puppet.com/docs/pdk/2.x/pdk_install.html 
* Clone repo and execute `pdk build`.  This will build the module to `pkg/newrelic-newrelic_installer-0.1.0.tar.gz`
* Copy `pkg/newrelic-newrelic_installer-0.1.0.tar.gz` to your master node and install manually
```shell
sudo puppet module install ~/newrelic-newrelic_installer-0.1.0.tar.gz
Notice: Preparing to install into /etc/puppetlabs/code/environments/production/modules ...
Notice: Downloading from https://forgeapi.puppet.com ...
Notice: Installing -- do not interrupt ...
/etc/puppetlabs/code/environments/production/modules
└─┬ newrelic-newrelic_installer (v0.1.0)
  ├── lwf-remote_file (v1.1.3)
  └── puppetlabs-powershell (v5.2.0)
```
## Getting Started 
To use this module, you'll need to instantiate the `::install` class, specifying an instrumentation target and some New Relic account-specific details.  For example:
```ruby
# /etc/puppetlabs/code/environments/<YOUR_ENVIRONMENT>/manifests/sites.pp
class { 'newrelic_installer::install':
          targets               => ["infrastructure"],
          environment_variables => {
            "NEW_RELIC_API_KEY"    => "<YOUR-NR-API-KEY>",
            "NEW_RELIC_ACCOUNT_ID" => <YOUR-NR-ACCOUNT-ID>,
            "NEW_RELIC_REGION"     => '<US|EU>'
          }
}
```
### Parameters
#### `targets` _[String]_          
Specifies target to be instrumented with New Relic 
Supported values include:
* `'infrastructure'` - New Relic Infrastructure Agent
#### `environment_variables` _Hash_ 
Hash of environment variables to set prior to execution.
**The following keys and values are required:**
* `'NEW_RELIC_API_KEY`: your New Relic API key
* `'NEW_RELIC_ACCOUNT_ID`: your New Relic account id
* `'NEW_RELIC_REGION`: your New Relic account's region (`US` or `EU`)
#### `verbosity` _String_ (optional)
Specifies command output verbosity
Supported values include
* `debug`
* `trace`
#### `tags` _Hash_ (optional)
Hash of tags associated with entities instrumented with New Relic.  Examples:
* `{'environment' => 'production', 'version' => '1.2.3'}`
#### `proxy` _String_ (optional)
Sets the proxy server the agent should use. Examples:
* `https://myproxy.foo.com:8080`
* `http://10.10.254.254`
#### `timeout` _Integer_ (optional)
Sets the timeout in seconds for New Relic installations.  Default is 600

## Support
New Relic hosts and moderates an online forum where customers can interact with
New Relic employees as well as other customers to get help and share best
practices. Like all official New Relic open source projects, there's a related
Community topic in the New Relic Explorers Hub. You can find this project's
topic/threads here:

* [New Relic Documentation](https://docs.newrelic.com): Comprehensive guidance for using our platform
* [New Relic Community](https://discuss.newrelic.com/c/support-products-agents/new-relic-infrastructure): The best place to engage in troubleshooting questions
* [New Relic Developer](https://developer.newrelic.com/): Resources for building a custom observability applications
* [New Relic University](https://learn.newrelic.com/): A range of online training for New Relic users of every level
* [New Relic Technical Support](https://support.newrelic.com/) 24/7/365 ticketed support. Read more about our [Technical Support Offerings](https://docs.newrelic.com/docs/licenses/license-information/general-usage-licenses/support-plan).

## Contribute

We encourage your contributions to improve the `newrelic_installer` Puppet module! Keep in mind that when you submit your pull request, you'll need to sign the CLA via the click-through using CLA-Assistant. You only have to sign the CLA one time per project.


If you have any questions, or to execute our corporate CLA (which is required if your contribution is on behalf of a company), drop us an email at opensource@newrelic.com.

**A note about vulnerabilities**

As noted in our [security policy](../../security/policy), New Relic is committed to the privacy and security of our customers and their data. We believe that providing coordinated disclosure by security researchers and engaging with the security community are important means to achieve our security goals.

If you believe you have found a security vulnerability in this project or any of New Relic's products or websites, we welcome and greatly appreciate you reporting it to New Relic through [HackerOne](https://hackerone.com/newrelic).

If you would like to contribute to this project, review [these guidelines](./CONTRIBUTING.md).

## License
This project is licensed under the [Apache 2.0](http://apache.org/licenses/LICENSE-2.0.txt) License.
