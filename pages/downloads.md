---
title: Downloads
permalink: /downloads/
---

<script type="text/javascript">
/**
* Function that tracks a click on an outbound link in Google Analytics.
* This function takes a valid URL string as an argument, and uses that URL string
* as the event label.
*/
var gtagCallback = function(event) {
  var hrefUrl = event.target.getAttribute('href')
  if (event.ctrlKey || event.shiftKey || event.metaKey || event.which == 2) {
    var newWin = true;}

  // $(this) != this
  var url = window.location.protocol + "//accumulo.apache.org" + $(this).attr("id")
  if (newWin) {
    gtag('event', 'click', {
      'event_category': 'outbound',
      'event_label': url,
      'transport_type': 'beacon'
    });
    return true;
  } else {
    gtag('event', 'click', {
      'event_category': 'outbound',
      'event_label': url,
      'transport_type': 'beacon',
      'event_callback': function(){ window.location.href = hrefUrl; }
    });
    return false;
  }
};

$( document ).ready(function() {
  // check if gtag is loaded
  if (typeof gtag === 'function') {
    $('.download_external').click(gtagCallback);
  }
});

var updateLinks = function(mirror) {
  $('a[link-suffix]').each(function(i, obj) {
    $(obj).attr('href', mirror.replace(/\/+$/, "") + $(obj).attr('link-suffix'));
  });
};

var mirrorsCallback = function(json) {
  var htmlContent = '<div class="row"><div class="col-md-3"><h5>Select an Apache download mirror:</h5></div>' +
    '<div class="col-md-5"><select class="form-control" id="apache-mirror-select">';
  htmlContent += '<optgroup label="Preferred Mirror (based on location)">';
  htmlContent += '<option selected="selected">' + json.preferred + '</option>';
  htmlContent += '</optgroup>';
  htmlContent += '<optgroup label="HTTP Mirrors">';
  for (var i = 0; i < json.http.length; i++) {
    htmlContent += '<option>' + json.http[i] + '</option>';
  }
  htmlContent += '</optgroup>';
  htmlContent += '<optgroup label="FTP Mirrors">';
  for (var i = 0; i < json.ftp.length; i++) {
    htmlContent += '<option>' + json.ftp[i] + '</option>';
  }
  htmlContent += '</optgroup>';
  htmlContent += '<optgroup label="Backup Mirrors">';
  for (var i = 0; i < json.backup.length; i++) {
    htmlContent += '<option>' + json.backup[i] + '</option>';
  }
  htmlContent += '</optgroup>';
  htmlContent += '</select></div></div>';

  $("#mirror_selection").html(htmlContent);

  $( "#apache-mirror-select" ).change(function() {
    var mirror = $("#apache-mirror-select option:selected").text();
    updateLinks(mirror);
  });

  updateLinks(json.preferred);
};

// get mirrors when page is ready
var mirrorURL = window.location.protocol + "//accumulo.apache.org/mirrors.cgi"; // http[s]://accumulo.apache.org/mirrors.cgi
$(function() { $.getJSON(mirrorURL + "?as_json", mirrorsCallback); });

</script>

<div id="mirror_selection"></div>

Be sure to verify your downloads by these [procedures][VERIFY_PROCEDURES] using these [KEYS][GPG_KEYS].

## Current Releases

### 1.9.2 **latest**{: .label .label-primary }

The most recent Apache Accumulo&reg; release is version 1.9.2. See the [release notes][REL_NOTES_19].

{: .table }
| **Binary** | [accumulo-1.9.2-bin.tar.gz][BIN_19] | [ASC][ASC_BIN_19] | [SHA][SHA_BIN_19] |
| **Source** | [accumulo-1.9.2-src.tar.gz][SRC_19] | [ASC][ASC_SRC_19] | [SHA][SHA_SRC_19] |

#### 1.9 Documentation
* [README][README_19]
* [HTML User Manual][MANUAL_HTML_19]
* [Examples][EXAMPLES_19]
* [Javadoc][JAVADOC_19]


### 1.7.4

The most recent 1.7.x release of Apache Accumulo&reg; is version 1.7.4. See the [release notes][REL_NOTES_17] and [CHANGES][CHANGES_17].

{: .table }
| **Binary** | [accumulo-1.7.4-bin.tar.gz][BIN_17] | [ASC][ASC_BIN_17] | [SHA][SHA_BIN_17] |
| **Source** | [accumulo-1.7.4-src.tar.gz][SRC_17] | [ASC][ASC_SRC_17] | [SHA][SHA_SRC_17] |

#### 1.7 Documentation
* [README][README_17]
* [HTML User Manual][MANUAL_HTML_17]
* [Examples][EXAMPLES_17]
* [Javadoc][JAVADOC_17]

## Older releases

Older releases are listed in the [release archive][ARCHIVE_REL] and can be
downloaded from the [download archive][ARCHIVE_DOWN].

[VERIFY_PROCEDURES]: https://www.apache.org/info/verification "Verify"
[GPG_KEYS]: https://www.apache.org/dist/accumulo/KEYS "KEYS"
[ARCHIVE_DOWN]: https://archive.apache.org/dist/accumulo "Download Archive"
[ARCHIVE_REL]: {{ site.baseurl }}/release/ "Release Archive"

[ASC_BIN_17]: https://www.apache.org/dist/accumulo/1.7.4/accumulo-1.7.4-bin.tar.gz.asc
[ASC_SRC_17]: https://www.apache.org/dist/accumulo/1.7.4/accumulo-1.7.4-src.tar.gz.asc
[SHA_BIN_17]: https://www.apache.org/dist/accumulo/1.7.4/accumulo-1.7.4-bin.tar.gz.sha512
[SHA_SRC_17]: https://www.apache.org/dist/accumulo/1.7.4/accumulo-1.7.4-src.tar.gz.sha512

[ASC_BIN_19]: https://www.apache.org/dist/accumulo/1.9.2/accumulo-1.9.2-bin.tar.gz.asc
[ASC_SRC_19]: https://www.apache.org/dist/accumulo/1.9.2/accumulo-1.9.2-src.tar.gz.asc
[SHA_BIN_19]: https://www.apache.org/dist/accumulo/1.9.2/accumulo-1.9.2-bin.tar.gz.sha512
[SHA_SRC_19]: https://www.apache.org/dist/accumulo/1.9.2/accumulo-1.9.2-src.tar.gz.sha512

[BIN_17]: https://www.apache.org/dyn/closer.lua/accumulo/1.7.4/accumulo-1.7.4-bin.tar.gz
{: .download_external link-suffix="/accumulo/1.7.4/accumulo-1.7.4-bin.tar.gz" id="/downloads/accumulo-1.7.4-bin.tar.gz" }
[SRC_17]: https://www.apache.org/dyn/closer.lua/accumulo/1.7.4/accumulo-1.7.4-src.tar.gz
{: .download_external link-suffix="/accumulo/1.7.4/accumulo-1.7.4-src.tar.gz" id="/downloads/accumulo-1.7.4-src.tar.gz" }

[BIN_19]: https://www.apache.org/dyn/closer.lua/accumulo/1.9.2/accumulo-1.9.2-bin.tar.gz
{: .download_external link-suffix="/accumulo/1.9.2/accumulo-1.9.2-bin.tar.gz" id="/downloads/accumulo-1.9.2-bin.tar.gz" }
[SRC_19]: https://www.apache.org/dyn/closer.lua/accumulo/1.9.2/accumulo-1.9.2-src.tar.gz
{: .download_external link-suffix="/accumulo/1.9.2/accumulo-1.9.2-src.tar.gz" id="/downloads/accumulo-1.9.2-src.tar.gz" }

[README_17]: https://github.com/apache/accumulo/blob/rel/1.7.4/README.md
{: .download_external id="/1.7/README" }
[README_19]: https://github.com/apache/accumulo/blob/rel/1.9.2/README.md
{: .download_external id="/1.9/README" }

[JAVADOC_17]: {{ site.baseurl }}/1.7/apidocs/
{: .download_external id="/1.7/apidocs/" }
[JAVADOC_19]: {{ site.baseurl }}/1.9/apidocs/
{: .download_external id="/1.9/apidocs/" }

[MANUAL_HTML_17]: {{ site.baseurl }}/1.7/accumulo_user_manual "1.7 user manual"
[MANUAL_HTML_19]: {{ site.baseurl }}/1.9/accumulo_user_manual "1.9 user manual"

[EXAMPLES_17]: {{ site.baseurl }}/1.7/examples "1.7 examples"
[EXAMPLES_19]: {{ site.baseurl }}/1.9/examples "1.9 examples"

[CHANGES_17]: https://issues.apache.org/jira/browse/ACCUMULO/fixforversion/12339577 "1.7.4 CHANGES"

[REL_NOTES_17]: {{ site.baseurl }}/release/accumulo-1.7.4/ "1.7.4 Release Notes"
[REL_NOTES_19]: {{ site.baseurl }}/release/accumulo-1.9.2/ "1.9.2 Release Notes"

