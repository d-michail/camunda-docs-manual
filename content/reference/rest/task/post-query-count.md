---

title: 'Get Task Count (POST)'
weight: 40

menu:
  main:
    name: "Get List Count (POST)"
    identifier: "rest-api-task-post-list-count"
    parent: "rest-api-task"
    pre: "POST `/task/count`"

---


Retrieves the number of tasks that fulfill the given filter.
Corresponds to the size of the result set of the [Get Tasks (POST)]({{< ref "/reference/rest/task/post-query.md" >}}) method and takes the same parameters.

{{< note title="Security Consideration" class="warning" >}}
  There are several query parameters (such as `assigneeExpression`) for specifying an EL expression. These are disabled by default to prevent remote code execution. See the section on <a href="{{< ref "/user-guide/process-engine/securing-custom-code.md">}}">security considerations for custom code</a> in the user guide for details.
{{</note>}}

# Method

POST `/task/count`


# Parameters

## Request Body

A JSON object with the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>taskId</td>
    <td>Restrict to task with the given id.</td>
  </tr>
  <tr>
    <td>taskIdIn</td>
    <td>Restrict to tasks with any of the given ids.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>Restrict to tasks that belong to process instances with the given id.</td>
  </tr>
  <tr>
    <td>processInstanceIdIn</td>
    <td>Restrict to tasks that belong to process instances with the given ids.</td>
  </tr>
  <tr>
    <td>processInstanceBusinessKey</td>
    <td>Restrict to tasks that belong to process instances with the given business key.</td>
  </tr>
  <tr>
    <td>processInstanceBusinessKeyExpression</td>
    <td>Restrict to tasks that belong to process instances with the given business key which is described by an expression.
     See the
     <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">user guide</a>
     for more information on available functions.</td>
  </tr>
  <tr>
    <td>processInstanceBusinessKeyIn</td>
    <td>Restrict to tasks that belong to process instances with one of the give business keys.
        The keys need to be in a comma-separated list.
    </td>
  </tr>
  <tr>
    <td>processInstanceBusinessKeyLike</td>
    <td>Restrict to tasks that have a process instance business key that has the parameter value as a substring.</td>
  </tr>
  <tr>
    <td>processInstanceBusinessKeyLikeExpression</td>
    <td>Restrict to tasks that have a process instance business key that has the parameter value as a substring and is
    described by an expression. See the
    <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">user guide</a>
    for more information on available functions.</td>
  </tr>
  <tr>
    <td>processDefinitionId</td>
    <td>Restrict to tasks that belong to a process definition with the given id.</td>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>Restrict to tasks that belong to a process definition with the given key.</td>
  </tr>
  <tr>
    <td>processDefinitionKeyIn</td>
    <td>Restrict to tasks that belong to a process definition with one of the given keys.
        The keys need to be in a comma-separated list.
    </td>
  </tr>
  <tr>
    <td>processDefinitionName</td>
    <td>Restrict to tasks that belong to a process definition with the given name.</td>
  </tr>
  <tr>
    <td>processDefinitionNameLike</td>
    <td>Restrict to tasks that have a process definition name that has the parameter value as a substring.</td>
  </tr>
  <tr>
    <td>executionId</td>
    <td>Restrict to tasks that belong to an execution with the given id.</td>
  </tr>
  <tr>
    <td>caseInstanceId</td>
    <td>Restrict to tasks that belong to case instances with the given id.</td>
  </tr>
  <tr>
    <td>caseInstanceBusinessKey</td>
    <td>Restrict to tasks that belong to case instances with the given business key.</td>
  </tr>
  <tr>
    <td>caseInstanceBusinessKeyLike</td>
    <td>Restrict to tasks that have a case instance business key that has the parameter value as a substring.</td>
  </tr>
  <tr>
    <td>caseDefinitionId</td>
    <td>Restrict to tasks that belong to a case definition with the given id.</td>
  </tr>
  <tr>
    <td>caseDefinitionKey</td>
    <td>Restrict to tasks that belong to a case definition with the given key.</td>
  </tr>
  <tr>
    <td>caseDefinitionName</td>
    <td>Restrict to tasks that belong to a case definition with the given name.</td>
  </tr>
  <tr>
    <td>caseDefinitionNameLike</td>
    <td>Restrict to tasks that have a case definition name that has the parameter value as a substring.</td>
  </tr>
  <tr>
    <td>caseExecutionId</td>
    <td>Restrict to tasks that belong to a case execution with the given id.</td>
  </tr>
  <tr>
    <td>activityInstanceIdIn</td>
    <td>Only include tasks which belong to one of the passed activity instance ids.</td>
  </tr>
  <tr>
    <td>tenantIdIn</td>
    <td>Restrict to tasks that belong to one of the given tenant ids.
        The ids need to be in a comma-separated list.</td>
  </tr>
  <tr>
    <td>withoutTenantId</td>
    <td>Only include tasks which belong to no tenant. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>assignee</td>
    <td>Restrict to tasks that the given user is assigned to.</td>
  </tr>
  <tr>
    <td>assigneeExpression</td>
    <td>Restrict to tasks that the user described by the given expression is assigned to.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
    </td>
  </tr>
  <tr>
    <td>assigneeLike</td>
    <td>Restrict to tasks that have an assignee that has the parameter value as a substring.</td>
  </tr>
  <tr>
    <td>assigneeLikeExpression</td>
    <td>Restrict to tasks that have an assignee that has the parameter value described by the given
expression as a substring.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
    </td>
  </tr>
  <tr>
    <td>assigneeIn</td>
    <td>Only include tasks which are assigned to one of the user ids passed in the array.</td>
  </tr>
  <tr>
    <td>assigneeNotIn</td>
    <td>Only include tasks which are not assigned to one of the user ids passed in the array.</td>
  </tr>
  <tr>
    <td>owner</td>
    <td>Restrict to tasks that the given user owns.</td>
  </tr>
  <tr>
    <td>ownerExpression</td>
    <td>Restrict to tasks that the user described by the given expression owns.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
    </td>
  </tr>
  <tr>
    <td>candidateGroup</td>
    <td>Only include tasks that are offered to the given group.</td>
  </tr>
  <tr>
    <td>candidateGroupExpression</td>
    <td>Only include tasks that are offered to the group described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
    </td>
  </tr>
  <tr>
    <td>candidateUser</td>
    <td>Only include tasks that are offered to the given user or to one of his groups.</td>
  </tr>
  <tr>
    <td>candidateUserExpression</td>
    <td>Only include tasks that are offered to the user described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
    </td>
  </tr>
  <tr>
    <td>includeAssignedTasks</td>
    <td>
      Also include tasks that are assigned to users in candidate queries. Default is to only include tasks that are not assigned to any user
      if you query by candidate user or group(s).
    </td>
  </tr>
  <tr>
    <td>involvedUser</td>
    <td>Only include tasks that the given user is involved in.
    A user is involved in a task if an identity link exists between task and user (e.g., the user is the assignee).</td>
  </tr>
  <tr>
    <td>involvedUserExpression</td>
    <td>Only include tasks that the user described by the given expression is involved in.
        A user is involved in a task if an identity link exists between task and user (e.g., the user is the assignee).
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">user
        guide</a> for more information on available functions.
    </td>
  </tr>
  <tr>
    <td>assigned</td>
    <td>If set to <code>true</code>, restricts the query to all tasks that are assigned.</td>
  </tr>
  <tr>
    <td>unassigned</td>
    <td>If set to <code>true</code>, restricts the query to all tasks that are unassigned.</td>
  </tr>

  <tr>
    <td>taskDefinitionKey</td>
    <td>Restrict to tasks that have the given key.</td>
  </tr>
  <tr>
    <td>taskDefinitionKeyIn</td>
    <td>Restrict to tasks that have one of the given keys.
      The keys need to be in a comma-separated list.
    </td>
  </tr>
  <tr>
    <td>taskDefinitionKeyLike</td>
    <td>Restrict to tasks that have a key that has the parameter value as a substring.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>Restrict to tasks that have the given name.</td>
  </tr>
  <tr>
    <td>nameNotEqual</td>
    <td>Restrict to tasks that do not have the given name.</td>
  </tr>
  <tr>
    <td>nameLike</td>
    <td>Restrict to tasks that have a name with the given parameter value as substring.</td>
  </tr>
   <tr>
    <td>nameNotLike</td>
    <td>Restrict to tasks that do not have a name with the given parameter value as substring.</td>
  </tr>
  <tr>
    <td>description</td>
    <td>Restrict to tasks that have the given description.</td>
  </tr>
  <tr>
    <td>descriptionLike</td>
    <td>Restrict to tasks that have a description that has the parameter value as a substring.</td>
  </tr>

  <tr>
    <td>priority</td>
    <td>Restrict to tasks that have the given priority.</td>
  </tr>
  <tr>
    <td>maxPriority</td>
    <td>Restrict to tasks that have a lower or equal priority.</td>
  </tr>
  <tr>
    <td>minPriority</td>
    <td>Restrict to tasks that have a higher or equal priority.</td>
  </tr>

  <tr>
    <td>dueDate</td>
    <td>Restrict to tasks that are due on the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.375+0200</code>.</td>
  </tr>
  <tr>
    <td>dueDateExpression</td>
    <td>Restrict to tasks that are due on the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>dueAfter</td>
    <td>Restrict to tasks that are due after the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.875+0200</code>.</td>
  </tr>
  <tr>
    <td>dueAfterExpression</td>
    <td>Restrict to tasks that are due after the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>dueBefore</td>
    <td>Restrict to tasks that are due before the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.037+0200</code>.</td>
  </tr>
  <tr>
    <td>dueBeforeExpression</td>
    <td>Restrict to tasks that are due before the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>withoutDueDate</td>
    <td>Only include tasks which have no due date. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>followUpDate</td>
    <td>Restrict to tasks that have a followUp date on the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.984+0200</code>.</td>
  </tr>
  <tr>
    <td>followUpDateExpression</td>
    <td>Restrict to tasks that have a followUp date on the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>followUpAfter</td>
    <td>Restrict to tasks that have a followUp date after the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.438+0200</code>.</td>
  </tr>
  <tr>
    <td>followUpAfterExpression</td>
    <td>Restrict to tasks that have a followUp date after the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>followUpBefore</td>
    <td>Restrict to tasks that have a followUp date before the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.847+0200</code>.</td>
  </tr>
  <tr>
    <td>followUpBeforeExpression</td>
    <td>Restrict to tasks that have a followUp date before the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>followUpBeforeOrNotExistent</td>
    <td>Restrict to tasks that have no followUp date or a followUp date before the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.746+0200</code>.</td>
  </tr>
  <tr>
    <td>followUpBeforeOrNotExistentExpression</td>
    <td>Restrict to tasks that have no followUp date or a followUp date before the date described by the given
        expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>createdOn</td>
    <td>
      Restrict to tasks that were created on the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.746+0200</code>.
    </td>
  </tr>
  <tr>
    <td>createdOnExpression</td>
    <td>Restrict to tasks that were created on the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>createdAfter</td>
    <td>Restrict to tasks that were created after the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.736+0200</code>.</td>
  </tr>
  <tr>
    <td>createdAfterExpression</td>
    <td>Restrict to tasks that were created after the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>createdBefore</td>
    <td>Restrict to tasks that were created before the given date. By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.037+0200</code>.</td>
  </tr>
  <tr>
    <td>createdBeforeExpression</td>
    <td>Restrict to tasks that were created before the date described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">
        user guide</a> for more information on available functions.
        The expression must evaluate to a <code>java.util.Date</code> or <code>org.joda.time.DateTime</code> object.
    </td>
  </tr>
  <tr>
    <td>delegationState</td>
    <td>Restrict to tasks that are in the given delegation state. Valid values are <code>PENDING</code> and <code>RESOLVED</code>.</td>
  </tr>
  <tr>
    <td>candidateGroups</td>
    <td>Restrict to tasks that are offered to any of the given candidate groups. Takes a JSON array of group names, so for example <code>["developers", "support", "sales"]</code>.</td>
  </tr>
  <tr>
    <td>candidateGroupsExpression</td>
    <td>Restrict to tasks that are offered to any of the candidate groups described by the given expression.
        See the <a href="{{< ref "/user-guide/process-engine/expression-language.md#internal-context-functions" >}}">user
        guide</a> for more information on available functions.
        The expression must evaluate to <code>java.util.List</code> of Strings.
    </td>
  </tr>
  <tr>
    <td>withCandidateGroups</td>
    <td>Only include tasks which have a candidate group. Value may only be <code>true</code>,
    as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>withoutCandidateGroups</td>
    <td>Only include tasks which have no candidate group. Value may only be <code>true</code>,
    as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>withCandidateUsers</td>
    <td>Only include tasks which have a candidate user. Value may only be <code>true</code>,
    as <code>false</code> is the default behavior.</td>
  </tr>
   <tr>
    <td>withoutCandidateUsers</td>
    <td>Only include tasks which have no candidate user. Value may only be <code>true</code>,
    as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>active</td>
    <td>Only include active tasks. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>Only include suspended tasks. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>taskVariables</td>
    <td>A JSON array to only include tasks that have variables with certain values. <br/>

    The array consists of JSON objects with three properties <code>name</code>, <code>operator</code> and <code>value</code>.
    <code>name</code> is the variable name, <code>operator</code> is the comparison operator to be used and <code>value</code> the variable value.<br/>
    <code>value</code> may be of type <code>String</code>, <code>Number</code> or <code>Boolean</code>.<br/>
    <br/>
    Valid operator values are: <code>eq</code> - equal to; <code>neq</code> - not equal to; <code>gt</code> - greater than;
    <code>gteq</code> - greater than or equal to; <code>lt</code> - lower than; <code>lteq</code> - lower than or equal to;
    <code>like</code>.<br/>
    </td>
  </tr>
  <tr>
    <td>processVariables</td>
    <td>A JSON array to only include tasks that belong to a process instance with variables with certain values.<br/>
    The array consists of JSON objects with three properties <code>name</code>, <code>operator</code> and <code>value</code>.
    <code>name</code> is the variable name, <code>operator</code> is the comparison operator to be used and <code>value</code> the variable value.<br/>
    <code>value</code> may be of type <code>String</code>, <code>Number</code> or <code>Boolean</code>.<br/>
    <br/>
    Valid operator values are: <code>eq</code> - equal to; <code>neq</code> - not equal to; <code>gt</code> - greater than;
    <code>gteq</code> - greater than or equal to; <code>lt</code> - lower than; <code>lteq</code> - lower than or equal to;
    <code>like</code>;<code>notLike</code>.<br/>
    </td>
  </tr>
  <tr>
    <td>caseInstanceVariables</td>
    <td>A JSON array to only include tasks that belong to a case instance with variables with certain values.<br/>
    The array consists of JSON objects with three properties <code>name</code>, <code>operator</code> and <code>value</code>.
    <code>name</code> is the variable name, <code>operator</code> is the comparison operator to be used and <code>value</code> the variable value.<br/>
    <code>value</code> may be of type <code>String</code>, <code>Number</code> or <code>Boolean</code>.<br/>
    <br/>
    Valid operator values are: <code>eq</code> - equal to; <code>neq</code> - not equal to; <code>gt</code> - greater than;
    <code>gteq</code> - greater than or equal to; <code>lt</code> - lower than; <code>lteq</code> - lower than or equal to;
    <code>like</code>.<br/>
    </td>
  </tr>
    <tr>
    <td>variableNamesIgnoreCase</td>
    <td>Match all variable names in this query case-insensitively. If set to <code>true</code> <code>variableName</code> and <code>variablename</code> are treated as equal.</td>
  </tr>
  <tr>
    <td>variableValuesIgnoreCase</td>
    <td>Match all variable values in this query case-insensitively. If set to <code>true</code> <code>variableValue</code> and <code>variablevalue</code> are treated as equal.</td>
  </tr>
  <tr>
    <td>parentTaskId</td>
    <td>Restrict query to all tasks that are sub tasks of the given task. Takes a task id.</td>
  </tr>
  <tr>
    <td>orQueries</td>
    <td>
    A JSON array of nested task queries with OR semantics. A task matches a nested query if it fulfills <i>at least one</i> of the query's predicates. With multiple nested queries, a task must fulfill at least one predicate of <i>each</i> query (<a href="https://en.wikipedia.org/wiki/Conjunctive_normal_form">Conjunctive Normal Form</a>).<br><br>

    All task query properties can be used except for: <code>sorting</code>, <code>withCandidateGroups</code>,
    <code>withoutCandidateGroups</code>, <code>withCandidateUsers</code>, <code>withoutCandidateUsers</code><br><br>

    See the <a href="{{< ref "/user-guide/process-engine/process-engine-api.md#or-queries" >}}">user guide</a>
    for more information about OR queries.
    </td>
  </tr>
</table>

\* For further information, please see the <a href="{{< ref "/reference/rest/overview/date-format.md" >}}"> documentation</a>.

# Result

A JSON object with a single count property.

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>count</td>
    <td>Number</td>
    <td>The number of tasks that fulfill the query criteria.</td>
  </tr>
</table>


# Response Codes

<table class="table table-striped">
  <tr>
    <th>Code</th>
    <th>Media type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>200</td>
    <td>application/json</td>
    <td>Request successful.</td>
  </tr>
  <tr>
    <td>400</td>
    <td>application/json</td>
    <td>Returned if some of the query parameters are invalid. See the <a href="{{< ref "/reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

POST `/task/count`

Request Body:

```json
{"taskVariables":
    [{"name": "varName",
    "value": "varValue",
    "operator": "eq"
    },
    {"name": "anotherVarName",
    "value": 30,
    "operator": "neq"}],
"processInstanceBusinessKeyIn": "aBusinessKey,anotherBusinessKey",
"assigneeIn": "anAssignee,anotherAssignee",
"priority":10}
```

## Response
```json
{"count":1}
```

## Request with OR queries

POST `/task/count`

Logical query: `assignee = "John Munda" AND (name = "Approve Invoice" OR priority = 5) AND (suspended = false OR taskDefinitionKey = "approveInvoice")`

Request Body:
```json
{
  "assignee": "John Munda",
  "orQueries": [
    {
      "name": "Approve Invoice",
      "priority": 5
    },
    {
      "suspended": false,
      "taskDefinitionKey": "approveInvoice"
    }
  ]
}
```

## Response
```json
{
  "count": 1
}
```