AC-PC校正：
将spm_cfg.m，spm_cfg_autoreorient.m复制到SPM\config\目录下

已知spm_cfg.m与原SPM目录修改部分为，spm_cfg_autoreorient.m未知
%--------------------------------------------------------------------------
% Spatial
%--------------------------------------------------------------------------
spatial.help    = {'Various spatial and other pre-processing functions.'};
spatial.values  = { spm_cfg_autoreorient spm_cfg_realign spm_cfg_realignunwarp spm_cfg_coreg spm_cfg_preproc8 spm_cfg_norm spm_cfg_smooth };


使用方法：
运行spm_auto_reorient.m,原文件有错误我修改后的：CN_of_spm_auto_reorient.m
第一次选择一个nii文件，点击done,
第二次选择所有需要批量处理的nii文件，点击done.就完成了。
注意校正后的文件直接覆盖原文件，所有最好备份原文件。
还有就是模态单独处理，不要把MRI和PET一起校正，
而是分开，并设置i_type = 'T1'; 为对应模态

！！！有些PET图像是4D的函数File_Split_4DTo3D.m提供方法转换为3D,根据需要选择指定切片
PET 扫描是动态的（即在特定时间间隔内多次成像），那么生成的图像数据可以是 4D 的