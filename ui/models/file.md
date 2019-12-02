# File

This object is intended to hold only metadata describing a file, including a reference to to real location of the file bits.

| Field | Type | Description |
| ----- | ---- | ----------- |
| **id** | URI | Object ID in Fedora. |
| **name** | string | a filename |
| **origin** | enum | <ul><li>~~`upload`: direct user upload.~~</li><li>`onedrive`: file was picked from the user's OneDrive.</li></ul>  _We currently do not support direct file upload_ |
| **status** | enum | <ul><li>`processing`: file is being processed. This could mean that it is being uploaded, scanned, or being reviewed by a person.</li><li>`changesRequired`: an entity has identified that this file must be changed or removed from the submission. This status should be associated with a [SubmissionAction](submissionAction.md) with type `file` in the submission.</li><li>`accepted`: the file has passed all automated and/or manual review.</li><li>`published`: the file is avaialble for public consuption in the discovery interface.</li></ul> |
| description | string | (Optional) human readable description of the file, provided by the user in the UI. |
| externalId | string | external reference to the file, if not a direct upload. This must be the file's OneDrive ID if the file was picked from the users OneDrive. |
| downloadUrl | URI | Required only for files where `origin === 'onedrive'`. The short-lived link that can be used to download the file. |
| externalPath | string | Required only for files where `origin === 'onedrive'`. File path of this file in OneDrive. This will be used to recreate the file hierarchy after it is downloaded. |
| checksum | string | checksum calculated for a file. |
| checksumFunction | string | Method used for the file checksum, e.g. `xor`, `sha256`, etc |
| size | int | file size in bytes(?) |
| location | string (URI?) | reference to the location of the bits in the system (for example: copied into scratch space). |
