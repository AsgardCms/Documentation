title: Events
subtitle: Media Module
-------

The following events are triggered in the Media Module:

- [FileWasUploaded](#file-was-uploaded)
- [FileWasLinked](#file-was-linked)
- [FileWasUnlinked](#file-was-unlinked)
- [FileWasCreated](#file-was-created)
- [FileWasUpdated](#file-was-updated)


## <a name="file-was-uploaded" class="anchor" href="#file-was-uploaded">FileWasUploaded</a>

Triggered when a file was uploaded. You have access to the complete [File entity](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Media/Entities/File.php).

## <a name="file-was-linked" class="anchor" href="#file-was-linked">FileWasLinked</a>

Triggered when a file was linked to an other entity. You have access to the complete [File entity](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Media/Entities/File.php) as well as the linked entity.

For instance if you link a cover image to your blog post, you'll have access to the file and to the post the file was linked too.

## <a name="file-was-unlinked" class="anchor" href="#file-was-unlinked">FileWasUnlinked</a>


Triggered when a file was unlinked from an entity. You have access to the imageable relation.

In this relation you have access to the `file_id`, the `type`, `type_id` and the `zone`.

## <a name="file-was-created" class="anchor" href="#file-was-created">FileWasCreated</a>

Triggered when a file was created. This event has a public `$file` property.

## <a name="file-was-updated" class="anchor" href="#file-was-updated">FileWasUpdated</a>

Triggered when a file was updated. This event has a public `$file` property.
