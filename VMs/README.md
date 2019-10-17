<p><strong><span style="font-size: 30px;">Instructions:</span></strong></p>
<p>
  <br>
</p>
<p><span style="font-size: 14px;">This Folder Contains linux bash scripts to manage VMs in the openstack environment.&nbsp;</span></p>
<p><span style="font-size: 14px;"><strong>Any added script should have a manual added to this readme file.</strong></span></p>
<p><span style="font-size: 14px;">The manual should contain the basics for using the script and preferably a help page for using the script.</span></p>
<p>
  <br>
</p>
<p>- spawnNVms: This script creates N vms each with a new network, subnet, and port. right now it is customized to only build vms with direct ports and the flavor m1.small, but in the future it will be generalized to build any kind on any availability zone (this is used in a tripleO deployment).</p>
<p>&nbsp; &nbsp; spawnNVms [starting Label] [VMs number] [availability zone index]: this script create N vms with the name formate "vm{Label}" starting from the staring Label and ending with "{Label}+{number of VMs-1}". the name of the networks will be in the format "private_vlan{Label}" and the type is vlan. The name of the subnets is in the format "private_subnet{Label}" and with subnet ranges of format "12.12.{Label}.0/24". The ports are of type direct and have the format "direct{Label}".</p>
<p>&nbsp; &nbsp; So spawingNVms 0 3 0, will create: one VM with Label=3 on availability zone, computesriov0: "private_vlan3" "private_subnet3" "direct3" "vm3"</p>
<p>
  <br>
</p>
<p>- spawnNVms_devstack: This is the same as spawnNVms, but modified for the devstack environment. in it no availability zone is required, and it is tightly coupled with a particular setup, so for the use of this script you should make sure to change the names of the images, flavors, physical-networks, and any other resources so that it is compatible with your environment. (in the future options to modify these parameters will be added).</p>
<p>
  <br>
</p>
<p>- deleteNVms: This script is the opposite of the spawnNVms, it deletes N VMs of the format "vm{Label}", the difference is that it only deletes the vms, if you want to also delete the port, then add the flag -p, this will search for a port associated with the VM and delete it. if you want to delete the network, then you should add the flag -n, this will search for the network that the port is connected to, and deletes it. any error in any step will cause the script to stop, so make sure that vms, ports, and networks can be deleted successfully by making sure that there is no other ports connected to the network.</p>
<p>
  <br>
</p>
<p>deleteNVms [Starting lable] [Vms number] &lt;options&gt;</p>
<p>
  <br>
</p>
<p>DeleteNVms: delete a number of sequent VMs [Vms number] in openstack enviroment starting from [Starting lable]</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;, eg. deleteNVms 0 1: deletes only a VM called "vm0" because the lable is 0 and the number is 1</p>
<p>
  <br>
</p>
<p>&lt;options&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; --port | -p: &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;deletes the first associated port of the vms</p>
<p>
  <br>
</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; --network | -n: &nbsp; &nbsp; &nbsp; &nbsp; deletes the network associated with the port of the vm,</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; if an error happens the command will stop the operation and exit</p>
<p>
  <br>
</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; --name &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;specify the name before the Label, eg. deleteNVms 3 1 --name name, will delete the vm named "name3"</p>
