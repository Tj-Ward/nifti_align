# nifti_align
Easily align 3d nifti volumes to a template using afni tools with one line. The only benefit to using this script is lazyness, so that you can align one or more files with a single line and not have any extreneous outputs. Works for All image types. Default expects a T1w skull stripped (SS) brain and uses an ACPC SS'd brain as the target (see below or code for details). You can easily replace it for any other template such as a non-SS'd brain, a "native" space head for longitudinal alignment, PET and T2/FLAIR types too, just use the NMI flag. Additional files such as masks can be transformed at the same time. At least one image should be selected for reslicing. 

Requires working AFNI tools installation.

   ***********************
   *** Nifty Align Tool **
   ***********************
    
   Align nifti images to a template using rigid transformation
    
   Do not use periods (.) in image names, all text after the first (.) is treated as an extension
    
   Some more comments are available in the script. This isn't well written or anything.
   A better approach would be re-writing @auto_tlrc which is itself a wraper of AFNI tools
   This is better than using 3dwarpdrive or other registration tools I have found because it uses
   Nonlinear warping to find the alignment, then it estimates a rigid-body transformation to fit
    
   All credit goes to the AFNI team, this is just a dumb script to automate a few things.
   -tjw
     
      options:
      -h, --help                    Show brief help
      -i, --input       <path>      Input T1 (brainmask)
         *--skullstrip*             *Don't use* Skull strip flag (optional)
                                      Does not work well and adds too much time.
                                      Use template with skull instead
                                      Example: spmdefault_1mm_MNI_avg152T1.nii
          --template    <path>      Template to align to (optional)
                                      Default template is skullstripped TT_N27_brainmask.nii
                                      Either SS your input or use SS'd vol
                                      SS alignment is more accurate/reliable.
      -n, --nearest     <path>      Reslice img with NN
      -l, --linear      <path>      Reslice img with trilinear
          --keepmat                 Keep the afni transformation matrix
          --prefix      <str>       Prefix for output (default: 'a_')
          --nmi                     NMI cost funct. Default is lpc, good for T1w
                                      Good for PET alignment
                                    AFNI offers many good cost functions, just edit the
                                      script if you want to use a different one
