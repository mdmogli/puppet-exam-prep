# Templating using embedded puppet

[INDEX](../../README.md)

## Overview
Embedded Puppet (EPP) is a templating language based on the Puppet language.

### Example
```yaml
<%- | Boolean $keys_enable,
      String  $keys_file,
      Array   $keys_trusted,
      String  $keys_requestkey,
      String  $keys_controlkey
| -%>
<% if $keys_enable { -%>

    <%# Printing the keys file, trusted key, request key, and control key: -%>
    keys <%= $keys_file %>
    <% unless $keys_trusted =~ Array[Data,0,0] { -%>
        trustedkey <%= $keys_trusted.join(' ') %>
    <% } -%>
    <% if $keys_requestkey =~ String[1] { -%>
        requestkey <%= $keys_requestkey %>
    <% } -%>
    <% if $keys_controlkey =~ String[1] { -%>
        controlkey <%= $keys_controlkey %>
    <% } -%>
<% } -%>
```

## Calling epp template from puppet code:
EPP template text is processed by the two epp functions:

1. epp(template_name, optional_args_hash) - for evaluating an .epp file
2. inline_epp(epp_text_string, optional_args_hash) - for evaluating a string in EPP syntax

## Tags

```yaml
<% | PARAMETERS | %>: Declare the template’s parameters.
<%= EXPRESSION %>: Insert the value of a single expression.
<% EXPRESSION %>: Execute an expression without inserting a value.
<%# COMMENT %>: Add a comment.
```
## Variables:

Templates have two ways to use data:
1. Directly access class variables (local scope), such as $ntp::tinker:
```yaml
# MODULE_NAME/manifests/config.pp

  $config_content = epp('ntp/ntp.conf.epp')  # epp can access variables in global and local scope using $ntp::tinker way

  file { $ntp::config:
    ensure  => file,
    owner   => 0,
    group   => 0,
    mode    => $::ntp::config_file_mode,
    content => $config_content,
  }

```

```yaml
# MODULE_NAME/templates/ntp.conf.epp

<% if $ntp::tinker == true and ($ntp::panic or $ntp::stepout) { -%>
tinker<% if $ntp::panic { %> panic <%= $ntp::panic %><% } %><% if $ntp::stepout { -%> stepout <%= $ntp::stepout %><% } %>
<% } -%>

```
2. Use parameters passed at call time
```yaml
# MODULE_NAME/manifests/config.pp

  $config_content = epp('ntp/ntp.conf.epp', { $tinker, $stepout }) 

  file { $ntp::config:
    ensure  => file,
    owner   => 0,
    group   => 0,
    mode    => $::ntp::config_file_mode,
    content => $config_content,
  }

```

```yaml
# MODULE_NAME/templates/ntp.conf.epp

<% if $tinker == true  { -%>
tinker<% if $tinker { %> panic <%= $tinker %><% } %><% if $tinker { -%> stepout <%= $stepout %><% } %>
<% } -%>

```

**NOTE**: Special scope rule for **inline_epp**: If you evaluate a template with the inline_epp function, and if the template has no parameters, either passed or declared, you can access variables from the calling class in the template by using the variables’ short names. This exceptional behavior is only allowed if all of the above conditions are true.

## EPP validation and rendering:
```bash
    $ puppet epp validate example.epp
    $ puppet epp render example.epp --values '{x => 10, y => 20}'
```
