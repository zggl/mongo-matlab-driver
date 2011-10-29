This is a Matlab extension supporting access to MongoDB.

After cloning the repo, unpack mongo-c-driver-src.zip into this directory.
Use the files in this zip file rather than [mongo-c-driver](http://github.com/mongodb/mongo-c-driver),
 since a few minor tweaks were required to get it to work with Matlab.

Windows:

Load the solution into Visual Studio and build the dll.  The project properties may need to be edited
to include the locations where the Matlab include files and libs are.

Linux:

`~/10gen/mongo-matlab-driver$ make`

Note that Matlab requires gcc-4.3

-----
Once the libary is built,

Add the path of the driver to Matlab:
`> addpath /10gen/mongo-matlab-driver`

Then the test suite can be run with:
`> MongoTest`

For normal operation, load the library with:
`> MongoStart`

Documentation may be accessed within Matlab by:
`> doc Mongo % for instance`

though you may find it more convenient to examine the class files directly.  Matlab clutters up the
help somewhat with documention on methods inherited from 'handle'.

Unload the library with:
`> MongoStop`

(you may have to clear variables in order to do this)

BASIC USAGE:

Connecting to a MongoDB server running on localhost is as straight forward and simple as:
mongo = Mongo();
This creates an instance of the Mongo class which you�ll use for subsequent communication with MongoDB.
Once you have established the connection, you may execute CRUD operations on the database quite easily. Simplified prototypes for these look like this:

`mongo.insert(namespace, record);`
`result = mongo.findOne(namespace, query);`
`mongo.update(namespace, criteria, objNew);`
`mongo.remove(namespace, criteria);`

namespace is the name of the collection on which to perform the operation.

A simple example of an actual insert looks like this:
`bb = BsonBuffer;
bb.append('name', 'John');
bb.append('age', int32(34));
bb.append('address', '1033 Vine Street');
record = bb.finish();
mongo.insert('test.people', record);`
