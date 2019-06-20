# waf

Role for managing AWS Web Application Firewalls

# Variables

* `waf_conditions` - list of WAF conditions with `name`, `filters` and `type` keys.
  `filters` is a list of filters with keys specific to type (see `ansible-doc aws_waf_condition` for examples)

* `waf_rules` - list of WAF rules with `name`, and `conditions` keys.
  `conditions` is a list of conditions, with the following keys:
  * `name` - the name of the condition
  * `type` - the type of the condition
  * `negated` - whether the rule should reverse the sense of the condition

* `waf_web_acl` - a dict describing the web ACL to manage, containing:
  * `name` - the name of the web acl
  * `default_action` - what to do when no rules match
  * `rules` - a list of rule dicts, containing:
    * `name` - name of the rule
    * `priority` - a unique number in the list of rules. Lower numbers are processed first
    * `action` - what to do if the rule matches

* `waf_regions` - List of regions that the waf will be created. Default is
  create WAF suitable for CloudFront distribution which is `us-east-1`
  To create WAF for the LoadBalancer you have to set the region as the same for
  the LoadBalancer
  As of this time the ansible waf module does not have an option to associate
  with the LoadBalancer thus it needs to be done manually or using aws cli. This
  can be done in the actual playbook.
