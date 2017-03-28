# Frequently Asked Questions

## Can I access the Vicon data from the eduroam or robots wifi networks?
To our knowledge no. You must plug in through ethernet in the local network or through a wireless router connected to the local network. The reason is that there is a firewall between our subnet and the `robots` network. We've been told by an IT guy that we can ask them to open some ports for us to get ssh and vicon data to passthrough. We are still reviewing this option. 

## Do I really need to cover the floor before using mocap?

Yes. The floor is far too reflective and creates lots of noise in the Vicon data. Ideally also get rid of/cover up metallic objects that can reflect infrared light.

## How many markers do I need to put on my vehicle for it to be recognized as an object?

Minimum 3, try to space them out on all axes and place them in a non-symmetric pattern. Ideally in a way that the markers are all visible from every viewpoint.

## What if I have a question that no one in the lab can answer?

Our point of contact is Felix Tsui (he installed the cameras in the lab) his contact information is taped on top of the server. 
