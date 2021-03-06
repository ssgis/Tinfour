Tinfour
========

High-Performance 2D Delaunay Triangulation and Related Utilities Written in Java

**Notice**

> Effective with software release 2.1 (June 2019), Tinfour includes
> a "fat jar" with bundled dependencies that greatly simplifies
> the execution of the demonstration TinfourViewer application.
> See [Tinfour Execution](https://github.com/gwlucastrig/Tinfour/wiki/Tinfour-Execution-from-the-Command-Line) for more details.
>
> Effective with release 2.1, Tinfour now includes a version of the
> [Simple Volumetric Model](https://github.com/gwlucastrig/Tinfour/wiki/Using-the-Delaunay-to-Create-a-Reservoir-Volume-Model)
> a demonstration program that can be used to compute reservoir capacity and water volume
> as a function of water level.
>
> The Tinfour compiled binary files (Jar files) are available at
> [Sonatype's Maven Central Repository](https://search.maven.org/search?q=Tinfour)
> or the [Maven Central Repository](http://central.maven.org/maven2/org/tinfour/)

### Delaunay Triangulation ###
The Delaunay Triangulation defines an optimal form for organizing unstructured or semi-random
sample points into a triangular mesh. That optimality makes the Delaunay Triangulation
a useful tool for interpolation, grid construction, and surface analysis.  

![Surface Models using TINs](doc/images/TwoTins.png "Surface Models using TINs")

### Tinfour ###
Tinfour is a software library written in Java that provides tools for constructing 
and applying Triangulated Irregular Networks (TINs) that conform to the Delaunay
criterion. Because it is intended to process large data sets,
the implementation gives a great deal of attention to performance and
memory use. On a conventional laptop, Tinfour is capable of processing sample
points at a rate of better than one million points per second.

The Tinfour source code includes extensive documentation. This project also includes
an informal paper that describes the uses, algorithms, and implementation
of the software with enough detail to support potential developers 
who may wish to contribute code or employ Tinfour in their own work. For more details, see
[Data Elements and Algorithms for the Tinfour Libary](http://gwlucastrig.github.io/Tinfour/doc/TinfourAlgorithmsAndDataElements.pdf "Data Elements and Algorithms").
The Tinfour API documentation is available at [Tinfour API](http://gwlucastrig.github.io/Tinfour/doc/javadoc/ "Javadoc for Tinfour API").
And, to support our user community, we've recently started a mailing list at the [Tinfour Users Group](https://groups.google.com/forum/#!forum/tinfour-users-group). 

### The Tinfour Viewer ###
When someone first sees a project like Tinfour, they might reasonably ask
that most thorny of questions "What is it good for?"  To try to address that question,
this library includes a simple demonstration program which allows the user to view
and explore raw data, including samples such as Lidar files that contain
huge numbers of points. To run the demonstrator, you must have Java installed
on your system.  If you do not have Java installed on your computer, you may
download an installer for free from 
[Oracle Corporation, Java Downloads](https://java.com/en/download/ "Java downloads from Oracle")

Instructions for setting up and running the Tinfour Viewer application
are provided at the wiki page [Tinfour Execution from the Command Line](https://github.com/gwlucastrig/Tinfour/wiki/Tinfour-Execution-from-the-Command-Line).
With the introduction of the _fat jar_ feature in recent releases, the procedure for
launching the Tinfour Viewer became much simpler. For example, if you have Java installed
on a Windows system, you can launch the Tinfour Viewer application from your File Explorer window
by double-clicking on the "fat" jar file TinfourDemo-2.1.2-jar-with-dependencies
(adjusting the version as appropriate). 
While other Tinfour applications must be launched from the command-line,
the wiki page attempts to simplify the process as much as possible. It also
explains some of the nuances of the launch procedures and provides the details
you will need to set up a command window and run the command-line variations
for all the various Tinfour applications.
 
The demonstrator is intended to show how the Tinfour library could be integrated
into a full-featured GIS application or other analysis tool. It's a simple
implementation with a minimum of features. 

![Lidar over Guilford, CT](doc/images/TinfourViewerGuilford.jpg "Lidar over Guilford, CT")

### Sources of Data ###
Lidar is a system for collecting surface elevation using laser measuring devices
mounted on low flying aircraft. It's pretty amazing technology.
There are some excellent sources of Lidar data to be had for free, you might start at 
[Free LiDAR Data Sources](http://gisgeography.com/top-6-free-lidar-data-sources/ "Gis Geography")
or [USGS Center for LIDAR Information] (http://lidar.cr.usgs.gov/ "USGS").
The Commonwealth of Pennsylvania was one of the first states to collect and post
a comprehensive survey of lidar data, and they did the job right... Their site includes 
not just lidar data, but the supporting breakline files (Shapefiles), multi-spectral imagery,
and project metadata (including Dewberry reports). Visit this excellent resource at
[PAMAP Lidar Elevation Data]( http://www.dcnr.state.pa.us/topogeo/pamap/lidar/index.htm "PAMAP Lidar Elevation Data").

If you just want to download a single Lidar file and view it, I recommend PAMAP Tile 4100133PAS
ftp://pamap.pasda.psu.edu/pamap_lidar/cycle1/LAS/South/2006/40000000/41001330PAS.zip
At 36.7 megabytes, it isn't dainty, but it does contain interesting land features and sufficient
detail to exercise the major functions of the viewer.

### A short demo ###
Recently, I found an earlier Delaunay triangulation project by "The Mad Creator" (Bill Dwyer)
that provided a four-line demo. It was such a elegant way of introducing the package,
that I decided to include one of my own.


```Java
  public static void main(String []args) throws Exception {
      IncrementalTin tin = new IncrementalTin(1.0);
      List<Vertex>vertexList = TestVertices.makeRandomVertices(100, 0);
      tin.add(vertexList, null);
      TinRenderingUtility.drawTin(tin, 500, 500, new File("tin.png"));
  }
``` 


### Does Tinfour require external project dependencies? ###
The core Tinfour module has no external dependencies. All it requires
is the standard Java API. Thus, you can integrate the core classes
into your own applications without adding unnecessary object code to
your software.

The associated, extended-functionality modules do depend on object code from external projects.
These include modules that can read data from Geographic Information System (GIS) sources
(Shapefiles and airborne Lidar LAS files) and those that perform advanced mathematical
and statistical analysis. These modules and dependencies are described in the Tinfour wiki page
[Tinfour Builds and Dependencies](https://github.com/gwlucastrig/Tinfour/wiki/Tinfour-Builds-and-Dependencies).


### What version of Java is required for Tinfour? ###
Tinfour is compiled under Java 8.   

### Configuring Tinfour in an IDE ###
In terms of its software and package organization, Tinfour has a relatively simple structure, so opening
it in an Integrated Development Environment (IDE) is straight forward.
The major Java IDEs (Netbeans, Eclipse, and IntelliJ) all support direct access to Maven projects.
If you have one of these IDE's you can simply load the Tinfour project and run with it. All work fine.
More hints and background information on configuring Tinfour for use in an IDE are included in the Tinfour wiki page
[Tinfour Builds and Dependencies](https://github.com/gwlucastrig/Tinfour/wiki/Tinfour-Builds-and-Dependencies).
 
### Current Work ###
The most recent addition to the Tinfour package is support for Voronoi Diagrams.
We've also added a new article on [Natural Neighbor Interpolation](https://github.com/gwlucastrig/Tinfour/wiki/Introduction-to-Natural-Neighbor-Interpolation)
to our wiki.

The current focus of Tinfour development is polishing aspects
of the Constrained Delaunay Triangulation (CDT) implementation. The CDT
is a technique for representing discontinuities in a Triangulated Irregular Network.
For example, geographic applications often need a way to represent "breaklines" -- features including
rivers, roads, coastlines and escarpments -- which mark a sudden change in
the local slope or terrain. Conventional Delaunay Triangulations
have a limited ability to treat boundaries where the surface undergoes a
nearly instantaneous change.  By introducing linear and polygon features to
the construction of a TIN, the Constrained Delaunay Triangulation provides
an effective way of representing such features. For an illustrated discussion
of why CDT's are important, see the Tinfour wiki page titled
[About the Constrained Delaunay Triangulation](https://github.com/gwlucastrig/Tinfour/wiki/About-the-Constrained-Delaunay-Triangulation "About the Constrained Delaunay Triangulation")

For more detail about the Tinfour project development plans, see the
[Tinfour Project Status and Roadmap](https://github.com/gwlucastrig/Tinfour/wiki/Tinfour-Project-Roadmap) page.
 
### Out Companion Project ###
Visit the [Gridfour Software Project](https://gwlucastrig.github.io/gridfour/) to learn more about our companion
software project dedicated to creating open-source software tools for raster (grid) data sets.

### Conclusion ###
Finally, the whole point of working on a project like Tinfour is to see 
it used to do something useful. To that end, I welcome ideas, requests, and
recommendations for analysis tools and applications that would
benefit the open source and scientific communities. Got something
to say? You can contact me at <contact.tinfour@gmail.com>
 
