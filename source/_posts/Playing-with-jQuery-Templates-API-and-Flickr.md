title: Playing with jQuery Templates API and Flickr
date: 10/5/2010 9:30:02 AM
updated: 10/5/2010 9:30:02 AM
tags: ["jQuery"]
---
Last week I spent some time playing with the today’s [announced jQuery Templates API](http://blog.jquery.com/2010/10/04/new-official-jquery-plugins-provide-templating-data-linking-and-globalization/)       
It was funny to see the different announcement tonight; [Scott](http://weblogs.asp.net/scottgu/archive/2010/10/04/jquery-templates-data-link-and-globalization-accepted-as-official-jquery-plugins.aspx), [JQuery Blog](http://blog.jquery.com/2010/10/04/new-official-jquery-plugins-provide-templating-data-linking-and-globalization/), [James](http://www.jamessenior.com/2010/09/30/jquery-templating-in-the-wild/)…

Tonight I have spent a bit more time with it and decided to adapt the sample I found here : “[Enabling JSONP calls on ASP.NET MVC](http://blogorama.nerdworks.in/entry-EnablingJSONPcallsonASPNETMVC.aspx)” to use JQuery Templates

I used [JetBrains WebStorm](http://www.jetbrains.com/webstorm/) to develop and here is the result

<?xml version="<span style="color: #8b0000">1.0</span>" encoding="<span style="color: #8b0000">UTF-8</span>"?>
</pre>

<!DOCTYPE html
</pre>

        PUBLIC "<span style="color: #8b0000">-//W3C//DTD XHTML 1.0 Transitional//EN</span>"
</pre>

        "<span style="color: #8b0000">http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd</span>">
</pre>

<html xmlns="<span style="color: #8b0000">http://www.w3.org/1999/xhtml</span>" xml:lang="<span style="color: #8b0000">en</span>" lang="<span style="color: #8b0000">en</span>">
</pre>

<head>
</pre>

    <title>flickr JQuery Template</title>
</pre>

    <script type="<span style="color: #8b0000">text/javascript</span>" src="<span style="color: #8b0000">js/code.jquery.com%20jquery-1.4.2.js</span>"/>
</pre>

    <script type="<span style="color: #8b0000">text/javascript</span>" src="<span style="color: #8b0000">js/jquery-ui-1.8.5.custom.min.js</span>"/>
</pre>

    <script type="<span style="color: #8b0000">text/javascript</span>" src="<span style="color: #8b0000">js/jquery.tmpl.js</span>"/>
</pre>

</head>
</pre>

<body>
</pre>

</pre>

<script id="<span style="color: #8b0000">flickrTemplate</span>" type="<span style="color: #8b0000">text/html</span>">
</pre>

    <div>
</pre>

        <h2>${title}</h2>
</pre>

        <div>
</pre>

            <img src="<span style="color: #8b0000">http://farm5.static.flickr.com/${server}/${id}_${secret}_t.jpg</span>" 
</pre>

                  title="<span style="color: #8b0000">${title}</span>" 
</pre>

                  alt="<span style="color: #8b0000">${title}</span>" />
</pre>

        </div>
</pre>

    </div>
</pre>

</script>
</pre>

</pre>

    <div id="<span style="color: #8b0000">interesting_photos</span>"></div>
</pre>

</pre>

    <script type="<span style="color: #8b0000">text/javascript</span>">
</pre>

    <span style="color: #008000">//</span>
</pre>

    <span style="color: #008000">// Flickr REST url</span>
</pre>

    <span style="color: #008000">//</span>
</pre>

    <span style="color: #0000ff">var</span> url = "<span style="color: #8b0000">http://api.flickr.com/services/rest/?</span>";
</pre>

</pre>

    <span style="color: #008000">//</span>
</pre>

    <span style="color: #008000">// My Flickr API key</span>
</pre>

    <span style="color: #008000">//</span>
</pre>

    <span style="color: #0000ff">var</span> api_key = "<span style="color: #8b0000">--your flickr api key here--</span>";
</pre>

</pre>

    <span style="color: #008000">// get interesting photos</span>
</pre>

    <span style="color: #008000">//</span>
</pre>

    <span style="color: #0000ff">function</span> getInterestingPhotos() {
</pre>

        <span style="color: #008000">//</span>
</pre>

        <span style="color: #008000">// build the URL</span>
</pre>

        <span style="color: #008000">//</span>
</pre>

        <span style="color: #0000ff">var</span> call = url + "<span style="color: #8b0000">method=flickr.interestingness.getList&amp;api_key=</span>"
</pre>

                       + api_key
</pre>

                       + "<span style="color: #8b0000">&amp;per_page=5&amp;page=1&amp;format=json&amp;jsoncallback=?</span>";
</pre>

</pre>

        <span style="color: #008000">//</span>
</pre>

        <span style="color: #008000">// make the ajax call</span>
</pre>

        <span style="color: #008000">//</span>
</pre>

        $.getJSON(call, <span style="color: #0000ff">function</span>(rsp) {
</pre>

            <span style="color: #0000ff">if</span> (rsp.stat != "<span style="color: #8b0000">ok</span>") {
</pre>

                <span style="color: #008000">//</span>
</pre>

                <span style="color: #008000">// something went wrong!</span>
</pre>

                <span style="color: #008000">//</span>
</pre>

                $( "<span style="color: #8b0000">#interesting_photos</span>" ).append(
</pre>

                    "<span style="color: #8b0000">&lt;label style=\"color:red\"&gt;Whoops!  It didn't work!</span>" +
</pre>

                    "<span style="color: #8b0000">  This is embarrassing!  Here's what Flickr had to </span>" +
</pre>

                    "<span style="color: #8b0000"> say about this - </span>" + rsp.message + "<span style="color: #8b0000">&lt;/label&gt;</span>");
</pre>

            }
</pre>

            <span style="color: #0000ff">else</span> {
</pre>

                <span style="color: #008000">//</span>
</pre>

                <span style="color: #008000">// build the html</span>
</pre>

                <span style="color: #008000">//</span>
</pre>

                $("<span style="color: #8b0000">#flickrTemplate</span>")
</pre>

                        .tmpl(rsp.photos.photo)
</pre>

                        .appendTo( "<span style="color: #8b0000">#interesting_photos</span>" );
</pre>

            }
</pre>

        });
</pre>

    }
</pre>

    </script>
</pre>

</pre>

    <script type="<span style="color: #8b0000">text/javascript</span>">
</pre>

        $(<span style="color: #0000ff">function</span>() {
</pre>

            $(getInterestingPhotos);
</pre>

        })
</pre>

    </script>
</pre>

</pre>

</body>
</pre>

</html></pre>

I could have done a template also of error message.
