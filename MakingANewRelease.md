_Process to follow on making a new release of JIDT_

## Introduction

This page, intended for developers, outlines the process we follow in making a new release of JIDT:

 1. Check the PDFs for all Demos in the repository are up to date
 1. Update build.xml for the new version number
 1. Update readme.txt with release notes etc
 1. Build the releases in a clean svn download
 1. Check sha1 of the new release: `sha1sum infodynamics-dist-1.0.zip`
 1. Post the code to lizier.me, make new counter files, ready and chmod them via ssh access. (Can also chmod via a web ftp on siteground; but by copying old counter files they tend to have the right permissions already)
 1. Post the Javadocs to lizier.me and link from our [Documentation](Documentation) page
 1. Link to the new code on the [Downloads](Downloads) page, [Installation](Installation) page and the front page of the google code site
 1. Update the news on the front page about the release and with release notes
 1. Mail the mailing list
 1. Tweet about the new release
 1. Update jar to clojars