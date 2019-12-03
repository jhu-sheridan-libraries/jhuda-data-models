# Submission Action

This describes an action that the user must perform on this submission before it can be accepted, or identifies changes made by the honest broker or curator. The honest broker or metadata curator will do their work and create these objects where necessary to inform the user that they must do something.

| Field | Type | Description |
| ----- | ---- | ----------- |
| key | string | reference to a file ID or metadata (JSON) key. |
| type | enum | <ul><li>`metadata`</li><li>`file`</li></ul> |
| status | enum | <ul><li>`modified`: the metadata curator has modified the metadata field identified by "`key`."</li><li>`changeRequested`: the metadata curator or honest broker identified a metadata field or file that must be changed.</li></ul> |
| description | string | Human readable description of the action that must be performed by the submitter. For example, the honest broker will enter a description of what needs to change in a flagged file. |

## Example

Assume that the user filled out metadata on the submission and included a key-value: `{ “foo”: “bar” }`. The metadata curator reviewed this metadata and determined that they should modify this field to look like `{ “foo”: “Bar 2” }`. This then requires that the submitting user approve this change. A SubmissionAction representing this could look like:

``` javascript
{
  “key”: “foo”,
  “type”: “metadata”,
  “status”: “modified”,
  “description”: “Changed ‘bar’ to ‘Bar 2’ because it was fun”
}
```
