# Submission

The top level object encapsulating a logical grouping of data and metadata to be deposited to the data archive.


| Field | Type | Description |
| ----- | ---- | ----------- |
| user | string | an opaque string that can be used to uniquely identify the user that created the submission. Provided by the user service |
| status | enum | An overview of the current overall status of the submission [Submission Status](#submission-status) |
| metadataStatus | enum | Status describing the current state of the submission metadata. [Metadata Status](#metadata-status) |
| filesStatus | enum | This status summarizes the state of the files associated with this submission. [Files Status](#files-status) |
| metadata | string | A stringified JSON object with the submission/package level metadata. Must validate against the JSON schema (to be provided) |
| files | List[URI] | A list of (Fedora) [File](file.md) objects |
| accessUrl | URI | A public URL where someone can view this submission. The UI should never write to this field |
| requiredActions | List[URI] | A list of references to [SubmissionAction](submissionAction.md)s that must be addressed by the user |
| state |  |  |

## Submission Status

| Value | Description |
| ----- | ----------- |
| draft | The submission is still user editable. This also means that submission has not yet been deposited in the archive |
| requiresAction | One or more changes were requested from the honest broker and/or the metadata curator. This status will be set if the honest broker flags one or more files to be changed and/or the metadata curator flags one or more metadata fields |
| complete | The data archive now has custody of the submission's data and materials. The submission is now read only. For this status to be reached, both metadata and files statuses must be `approved` |
| published | The submission is publicly available through the discovery interface. `accessUrl` should be populated only when the submission has this status |

## Metadata Status

| Value | Description |  |
| ----- | ----------- | --- |
| na | The user has not reached the metadata step in the workflow, or no metadata has been entered |
| draft | Submission metadata are user editable |
| requiresAction | The metadata curator has flagged one or more metadata fields. The user must approve changes to the metadata or make changes to the metadata. This status should be associated with a SubmissionAction. This status should take precedence over other metadata statuses |  |
| approved | The metadata curator has approved the metadata. If a user makes a change to the metadata, the status must change to `draft` |

## Files Status

| Value | Description |
| ----- | ----------- |
| na | The user has not reached the Files step of the workflow or no files are associated with this submission |
| processing | One or more files are being uploaded/copied and/or one or more files are being scanned |
| requiresAction | The honest broker has determined that one or more files must be modified or removed from the submission. This status should take precedence over other files statuses |
| complete | All files associated with this submission have been approved. If the user adds or modifies any files at this point, the status must change to `processing` |
