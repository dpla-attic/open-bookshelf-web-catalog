# open-bookshelf-web-catalog
This repository contains configuration files for the open bookshelf web catalog. The web catalog uses a Docker image built from Library Simplified's [patron-facing catalog](https://github.com/NYPL-Simplified/circulation-patron-web). This is configured in Elastic beanstalk using [Dockerrun.aws.json](Dockerrun.aws.json). To update to a new version, modify the image's version number (in `nypl/patron-web:1.0.0`) in the file and upload it to Elastic beanstalk.

There is also a [custom CSS file](openbookshelf.css) used to configure the header and work around some bugs or problems in the application. The file is uploaded to S3 and made public, and the library configuration in the Open Bookshelf circulation manager contains the public link to the file. The S3 bucket also must be configured to use CORS headers.

There is currently work in progress to update the web catalog, and much of the application is likely to be changed. The CSS workarounds should be possible to remove once a new version is available, and the CSS to configure the header may need to be updated.

For reference, here are the bugs or problems:
- The application adds a "Catalog" link by default, that's redundant with the breadcrumbs and possibly confusing. It's currently not possible to configure this. (https://github.com/dpla/open-bookshelf-web-catalog/blob/master/openbookshelf.css#L22-L24)
- The "Report a problem link" is broken. (https://github.com/dpla/open-bookshelf-web-catalog/blob/master/openbookshelf.css#L36-L38)
- Entrypoints for formats like ebooks and audiobooks are included as breadcrumbs, so that the breadcrumbs end up saying "All Books > Book > Open Bookshelf". Entrypoints should be a separate toggle, and aren't necessary at all for Open Bookshelf since it only has ebooks. (https://github.com/dpla/open-bookshelf-web-catalog/blob/master/openbookshelf.css#L40-L46)
- There are bugs in the CSS for the background color of breadcrumbs, so that a different color can appear behind the text and on the bottom border. (https://github.com/dpla/open-bookshelf-web-catalog/blob/master/openbookshelf.css#L48-L54)
