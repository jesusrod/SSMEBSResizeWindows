# SSM-EBS-RootVolume-Resize-Windows
SSM automation that will resize EBS volumes and expand Windows root partition

Copyright (c) 2021. Amazon Web Services Ireland LTD. All Rights Reserved. AWS Enterprise Support Team Name : SSM-EBS-RootVolume-Resize-Windows Version : 1.1.0 Encoded : No Paramaters : None Platform : Any EC2 Associated Files: None Abstract : ReadMe Document Revision History : - 1.1.0 | 30/03/2021 Initial Version Author : Jesus Rodriguez

##################### Automation Stop and Start.################################################ YOU ACKNOWLEDGE AND AGREE THAT THE SCRIPT IS PROVIDED FREE OF CHARGE "AS IS" AND "AVAILABLE" BASIS, AND THAT YOUR USE OF RELIANCE UPON THE APPLICATION OR ANY THIRD PARTY CONTENT AND SERVICES ACCESSED THEREBY IS AT YOUR SOLE RISK AND DISCRETION. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

################################################################################################
SSM EBS Resize EBS Volume and expand primary paritition

Command will read the instance ID and how much the primary root volume should be extended (this number should be greater than existent size otherwise the automation will stop).

This SSM Automation documente will perform the following steps:

1) Get Instance Details - When entering InstanceID It will obtain the primary Root volume device name and the list of devices.

2) Get Root Volume ID - it will use the main root device id and will obtain volume 0 VolumeID.

3) Read Instance Tag - will retrieve the key:tag 'Name' from the Instace

3) CreateSnapshot - it will create a volume snapshot of the primary volume and will capture the snapshot id.

4) Verify Snapshot - it will wait until the snapshot is complete 

5) Modify Volume Size - it will use the Volume Size entered by the user and will modify the volume using the execute AWS API

6) Expand Volume - it will use runcommand to execute a powershell script to expand the primary partition 

There's a Step that will publish and SNS message to a previously defined topic to notify if steps complete, also if either of the critical steps fail, I've defined three different messages to notify which step failed.
