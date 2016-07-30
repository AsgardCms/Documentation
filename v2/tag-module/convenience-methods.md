title: Convenience methods
subtitle: Tag Module
-------

- [Scope: `withTag()`](#scope-with-tag)
- [Scope: `whereTag()`](#scope-where-tag)
- [Get all tags for an entity: `allTags()`](#all-tags-for-entity)
- [Delete tags for an entity](#delete-tags-for-entity)


## <a name="scope-with-tag" class="anchor" href="#scope-with-tag">Scope: `withTag()`</a>

Get all the entities with one of the given tag(s). Optionally specify the column on which to perform the search operation, defaults to the `slug` column.

Example in your repository :

``` .language-php
// Get all files with either of the 2 tags
$files = $this->file->withTag(['your-first-tag', 'some-other-tag'])->get();
```


## <a name="scope-where-tag" class="anchor" href="#scope-where-tag">Scope: `whereTag()`</a>


Get all the entities with the given tag(s). Optionally specify the column on which to perform the search operation, defaults to `slug` column.

Example in your repository :

``` .language-php
// Get all files with all given tags
$files = $this->file->whereTag(['your-first-tag', 'some-other-tag'])->get();

// Get all files with the given tag
$files = $this->file->whereTag('your-first-tag')->get();
```



## <a name="all-tags-for-entity" class="anchor" href="#all-tags-for-entity">Get all tags for an entity: `allTags()`</a>


You can fetch all the tags for an entity by using the `allTags()` method.

``` .language-php
$tags = $file->allTags();
```


## <a name="delete-tags-for-entity" class="anchor" href="#delete-tags-for-entity">Delete tags for an entity: `untag()`</a>

To remove all tags from your entity call the `untag()` method on it.

``` .language-php
$file->untag();
```

You can also pass in an array of tags (`Tag` entity) to remove specific tags. You shouldn't have to call this yourself.


