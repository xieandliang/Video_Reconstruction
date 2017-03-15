# Video_Reconstruction
Video_Reconstruction

程序演示说明

一．代码包中各文件功能说明
项目进行 MATLAB 仿真所需的程序包名为 myprograms，该程序包包含了项目运行所需的全部 matlab 代码。
1. 项目仿真时需要的视频图片放在程序包 myprograms 里的 image 文件夹里，视频图片格式为 pgm；采用的视频测试序列为CIF格式的标准测试序列Foreman、Football、Susie。
2.  myprograms 文件夹里所有 matlab 源程序实现功能的详细说明。
（1）Tools 文件夹里的文件（程序）为本项目的优化方案的实现提供了基础的小波变换基（文件夹waveletcdf97，文件夹WaveletSoftware）、测量矩阵(文件夹BCS—SPL-1.5-1中的GenerateProjection.m文件，文件夹MS-BCS-SPL-1.2-2中的GenerateProjection.m文件)、基于块测量的算法程序（文件夹BCS—SPL-1.5-1，文件夹MS-BCS-SPL-1.2-2）、基于块的小波采样的算法程序（文件夹BCS—SPL-1.5-1，文件夹MS-BCS-SPL-1.2-2）、衡量视频图片优化性能的峰值信噪比算法程序和结构相似性算法程序（文件夹BCS—SPL-1.5-1，文件夹MS-BCS-SPL-1.2-2，ssim.m文件）。下面详细介绍其中每一个程序文件夹的功能。
（a）BCS-SPL-1.5-1 文件夹里是基于分块测量的分布式视频压缩感知重构算法程序包，里面为用 BCS-SPL 算法重构视频图像所需的所有源程序代码。其中，GenerateProjection.m文件是分块随机测量矩阵；PSNR.m 文件里函数的功能是计算反映视频图像客观质量的峰值信噪比（Peak-Signal-Noise Ratio，PSNR）；其他的m文件为编码端程序实现和解码端程序实现。
（b）MS-BCS-SPL-1.2-2 文件夹里是基于分块的在小波域进行采样测量的视频压缩感知重构算法程序包，即将 BCS-SPL 算法用于小波变换每个分解等级的每一个子带，里面为用 MS-BCS-SPL 算法重构视频图像所需的所有源程序代码。GenerateProjection.m文件是测量矩阵；其他的m文件为编码端程序实现和解码端程序实现。
（c）waveletcdf97 文件夹是 97 小波变换的程序。
（d）WaveletSoftware 文件夹里是小波域 DWT 和 IDWT 等的程序。（e）ssim.m 是求两个连续视频图像帧之间的结构相似性的程序。
（2）下面为本项目优化的分布式视频压缩感知稀疏重健模型的算法程序。
（a）MH_BCS_SPL_Decoder.m 文件的功能是：以 DDWT 作为稀疏基，执行 MH-BCS-SPL重构算法，对原始图片的测量值进行重构，得到重构的视频图像和用 BCS-SPL 算法重构出的视频图像。
（b）MH_BCS_SPL_Multihypothesis_Predictions.m 文件里函数的功能是：用基于分块的多假设预测模型对当前视频图像帧进行预测，生成当前视频图像帧的边信息，该函数适用于测量率不是很低的时候，测量率大于等于 0.2。
（c）MH_BCS_SPL_Multihypothesis_Predictions_Fast.m 文件里的函数功能是：用基于分块的多假设预测的方法对当前视频图像帧进行预测，生成当前视频图像帧的边信息，该函数适用于测量率很低的时候，可用于测量率为 0.1 的时候，但测量率很低的时候不一定非得使用此函数。
（d）MH_BCS_SPL_Residual_Reconstruction.m 文件里的函数的功能是：用 BCS_SPL 算法进行基于多假设预测的非关键帧的残差重构，得到最终基于多假设预测的非关键视频帧的图像。
（e）MH_BCS_SPL_Test_Residual.m 文件里函数的功能是：在测量域计算非关键帧的残差值。
（f）RDWT.m 文件里的函数的功能是产生一个完备正交基 RDWT。当子块尺寸等于块尺寸时(bl   Bl ) ，多假设预测在一个冗余的 DWT（RDWT）中进行。
（g）run_experiment_mhbcsspl.m 文件里的函数功能是用MH-BCS-SPL 算法进行视频图像的重构，并计算反映视频图像客观质量的峰值信噪比（Peak-Signal-Noise Ratio，PSNR），表征算法复杂度的重构时间，以及得到 BCS-SPL 、MH-BCS-SPL 和MH-MS-BCS-SPL算法重构视频图像的PSNR值，重构时间和主观视觉效果图。
（h）run_experiment_mymhmsbcsspl.m 文件里的函数功能是用本项目改进算法进行视频图像的重构，采用基于双向最佳匹配策略的多假设预测模型进行分布式视频压缩感知重构，并计算反映视频图像客观质量的峰值信噪比（Peak-Signal-Noise Ratio，PSNR），表征算法复杂度的重构时间，以及得到MH-MS-BCS-SPL和本项目基于双向最佳匹配策略多假设预测算法的重构视频图像的主观视觉效果图。
（i）run_pxperiment_psnr.m 文件里的函数功能是绘制出在不同的重构方案中，各种基于分块的重构模型在5个采样率下非关键帧重构图像的峰值信噪比PSNR，用折线图更直观地显示了非关键帧重构图像的平均PSNR值随采样率的变化情况。
（j）run_pxperiment_reccontime.m 文件里的函数功能是绘制出在不同的重构方案中，各种基于分块的重构模型在5个采样率下非关键帧重构图像的平均重构时间，用折线图更直观地显示了非关键帧重构图像的平均重构时间随采样率的变化情况。
（k）README.m 文件是对项目进行MATLAB 仿真时，需要运行哪几个m 文件的简单说明。
二．程序演示说明（程序运行过程）
1.在MATLAB 中的setpath中导入myprograms。
2.运行run_experiment_mhbcsspl.m文 件和run_experiment_mymhmsbcsspl.m文件。仿真过程中，先将程序中的测量率即subrate值确定好。例如，要仿真测量率为0.2时程序最终呈现的结果，就要在程序中将subrate值改为0.2，然后保存运行即可，可以获得 PSNR值，重构时间和主观视觉效果图。
3.最后运行run_pxperiment_psnr.m 文件，可以得到各种基于分块的重构模型在5个采样率下非关键帧重构图像的峰值信噪比PSNR，用折线图更直观地显示了非关键帧重构图像的平均PSNR值随采样率的变化情况；
4.运行run_pxperiment_reccontime.m文件，可以得到各种基于分块的重构模型在5.个采样率下非关键帧重构图像的平均重构时间，用折线图更直观地显示了非关键帧重构图像的平均重构时间随采样率的变化情况。
