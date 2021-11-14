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
## Tags

```yaml
<% | PARAMETERS | %>: Declare the template’s parameters.
<%= EXPRESSION %>: Insert the value of a single expression.
<% EXPRESSION %>: Execute an expression without inserting a value.
<%# COMMENT %>: Add a comment.
```
## Variables:

Templates have two ways to use data:
1. Directly access class variables, such as $ntp::tinker
1. Use parameters passed at call time
   
## EPP validation and rendering:
```bash
    $ puppet epp validate example.epp
    $ puppet epp render example.epp --values '{x => 10, y => 20}'
```
