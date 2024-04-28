AMBER INSTALLATION IN LINUX - NCSA HPC 
1. Download Miniconda, install, and initialize #Dependencies
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
#initialize
~/miniconda3/bin/conda init bash
#restart terminal or shell
re-login 

2. Select Option 3: Getting source code in tar format from Ambermd.org https://ambermd.org/GetAmber.php by filling name and institution appropriately

3. Getting Amber22 for non-commerical use on Ambermd.org

4. Drag both (2 & 3) tar files to your home directory 

5. Extract 2 & 3 (in your home directory terminal or wherever)
tar xvfj AmberTools23.tar.bz2
tar xvfj Amber22.tar.bz2

6. Export and build
export AMBERHOME=~/amber22_src/
cd amber22_src/build/
#view and edit run_cmake
vi run_cmake #Change DMPI=FALSE -DCUDA=FALSE to TRUE and save
#load other dependencies available within the GPU-enabled HPC
module load openmpi cuda cmake
#run cmake
./run_cmake
#install
make install
#for make error
follow this http://archive.ambermd.org/202302/0117.html troubleshooting conversation by adding the below to your "CMakeLists.txt" file in amber22_src directory

#ADDED LINE TO FIX CUB ISSUE
add_compile_definitions(THRUST_IGNORE_CUB_VERSION_CHECK)

8. Source for execution
source /u/mlawal/amber22/amber.sh

9. Follow the job submission protocol for your supercomputer environ.
