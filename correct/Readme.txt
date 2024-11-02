AC-PC校正：
将spm_cfg.m，spm_cfg_autoreorient.m复制到SPM\config\目录下

已知spm_cfg.m与原SPM目录修改部分如下:
%--------------------------------------------------------------------------
% Spatial
%--------------------------------------------------------------------------
spatial.help    = {'Various spatial and other pre-processing functions.'};
spatial.values  = { spm_cfg_autoreorient spm_cfg_realign spm_cfg_realignunwarp spm_cfg_coreg spm_cfg_preproc8 spm_cfg_norm spm_cfg_smooth };


使用方法：
运行spm_auto_reorient.m,原文件有错误我修改后的：Reorient.m
选择所有需要批量处理的nii文件，可以右击选择全部，点击done.就完成了。
注意校正后的文件直接覆盖原文件，所有最好备份原文件。
还有就是模态单独处理，不要把MRI和PET一起校正，
而是分开，并设置i_type = 'T1'; 为对应模态MRI,PET则是i_type = 'pet'

必读
！！！运行会产生temp.nii，会自动删除，如果没有删除手动删除再运行

如果AC位置偏离太远，模板匹配不上报错：
        There is not enough overlap in the images
        to obtain a solution.
还是需要手动校正到大概位置才可以不然模板匹配不上
但是又很麻烦，所有center_origin=true,先将图像ac设置在图像中心，我这样设置后都能匹配上


！！！有些PET/fmri图像是4D的,函数File_Split_4DTo3D.m提供方法转换为3D,根据需要选择指定切片
有些PET 扫描是动态的（即在特定时间间隔内多次成像），那么生成的图像数据可以是 4D 的
解释：有些图像是时间序列扫描，每个指定时间扫描一次然后就会有多个时间序列的3D图像：4D,所有切片为3D处理
Main_Fun_Split_4DTo3D.m
可以保留指定切片或者全部切片volume_to_keep为保留切边的索引，确保其没有超过时间序列索引，为0则保留所有切片
如果输出目录不改会覆盖原文件！！！

出现错误：因为nii是4D，请用Main_Fun_Split_4DTo3D.分割为3D
Can not use more than one source image.
出错 CN_of_spm_auto_reorient>spm_auto_reorient (第 81 行)
    [M, scal] = spm_affreg(vg,vf,flags);
                ^^^^^^^^^^^^^^^^^^^^^^^
出错 CN_of_spm_auto_reorient (第 130 行)
spm_auto_reorient(p,i_type,p_other)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ 