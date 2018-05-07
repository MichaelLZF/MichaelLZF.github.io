---
layout:     post
title:      OpenGL ES2.0
subtitle:
date:       2018-03-10
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - OpenGLES
---

# 说明

当前是第一次直译版本

# glActiveTexture-选择活动纹理单元

void glActiveTexture(GLenum texture);

texture：指定要激活哪个纹理单元，要实现的纹理单元的数量必须有至少8个，纹理必须是GL_TEXTUREi中的一个，i的值从0到GL_MAX_COMBINED_TEXTURE_IMAGE_UNITS-1，初始值是GL_TEXTURE0。

# glAttachShader

void GLAttachShader(GLunit program, GLunit shader);

program：将指定的着色器对象附加到该程序对象
shader：指定要附加的着色器对象

# glBindAttribLocation

void glBindAttribLocation(GLunit program,GLunit index, const GLchar * name);

program：要关联的对程序对象的操作
index：指定要绑定的通用顶点属性的索引
name：要绑定索引的顶点着色器属性变量的名称--

# glBindBuffer

void glBindBuffer(GLenum target,GLunit buffer);

target:指定缓冲区对象绑定的目标，符号常量必须是GL_ARRAY_BUFFER 或 GL_ELEMENT_ARRAY_BUFFER. 
buffer:指定缓冲区对象的名称

# glBindFramebuffer

void glBindFramebuffer(GLenum target,GLunit framebuffer);

target:指定帧缓冲区对象绑定的目标，符号常量必须是GL_FRAMEBUFFER
framebuffer:指定帧缓冲区对象的名称

# glBindRendererbuffer

void glBindRendererbuffer(GLenum target,GLunit renderbuffer);

target:指定渲染缓冲区对象绑定的目标，符号常量必须是GL_RENDERBUFFER
renderbuffer:指定渲染缓冲区对象的名称

# glBindTexture

void glBindTexture(GLenum target,GLunit texture);

target:指定纹理要绑定到的激活纹理目标，必须是GL_TEXTURE_2D或GL_TEXTURE_CUBE_MAP. 
texture:指定纹理的名称

# glBlendColor

void glBlendColor(GLclamf red,GLclampf green,GLclampf blue,GLclampf alpha);

red green blue alpha混合组成GL_BLEND_COLOR

# glBlendEquation

void glBlendEquatio(GLenum mode);

mode:指定组合源和目标颜色的方式，它必须是`GL_FUNC_ADD、GL_FUNC_SUBTRACT或GL_FUNC_REVERSE_SUBTRACT`

# glBlendEquationSeparate

void GLBlendEquationSeparate(GLenum modeRGB,GLenum modeAlpha);

modeRGB:指定RGB的混合方式，即`GL_FUNC_ADD、GL_FUNC_SUBTRACT或GL_FUNC_REVERSE_SUBTRACT`
modeAlpha:指定alpha的混合方式，`GL_FUNC_ADD、GL_FUNC_SUBTRACT或GL_FUNC_REVERSE_SUBTRACT`

# glBlendFunc

void glBlendFunc(GLenum sfactor,GLenum dfactor);

sfactor:指定如何计算RGBA的源混合因子，`GL_ZERO, GL_ONE, GL_SRC_COLOR, GL_ONE_MINUS_SRC_COLOR, GL_DST_COLOR, GL_ONE_MINUS_DST_COLOR, GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA, GL_DST_ALPHA, GL_ONE_MINUS_DST_ALPHA, GL_CONSTANT_COLOR, GL_ONE_MINUS_CONSTANT_COLOR, GL_CONSTANT_ALPHA, GL_ONE_MINUS_CONSTANT_ALPHA, and GL_SRC_ALPHA_SATURATE. The initial value is GL_ONE. `

dfactor:指定如何计算RGBA的目标混合因子，`GL_ZERO, GL_ONE, GL_SRC_COLOR, GL_ONE_MINUS_SRC_COLOR, GL_DST_COLOR, GL_ONE_MINUS_DST_COLOR, GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA, GL_DST_ALPHA, GL_ONE_MINUS_DST_ALPHA, GL_CONSTANT_COLOR, GL_ONE_MINUS_CONSTANT_COLOR, GL_CONSTANT_ALPHA, GL_ONE_MINUS_CONSTANT_ALPHA, and GL_SRC_ALPHA_SATURATE. The initial value is GL_ONE. `

# glBlendFuncSeparate(GLenum srcRGB,GLenum dstRGB,GLenum src Alpha,GLenum dstAlpha);

类比glBlendEquationSeparate与glBlendFunc，此处是将RGB与Alpha的计算处理方式分开了。

# glBufferData

void glBufferData(GLenum target,GLsizeiptr size, const GLvoid * data, GLenum usage);

target:指定目标缓冲区对象，符号常量必须是GL_ARRAY_BUFFER或GL_ELEMENT_ARRAY_BUFFER
size:指定缓冲对象的新数据的存储的大小（以字节为单位）
data:指定将被复制到数据存储区中用于初始化的数据的指针，如果没有要复制的数据，则指定为NULL
usage:指定数据存储的预期使用模式，符号常量必须是GL_STREAM_DRAW、GL_STATIC_DRAW 或 GL_DYNAMIC_DRAW. 

# glBufferSubData

void glBufferSubData(GLenum target,GLintptr offset.GLsizeiptr size,const GLvoid * data);

target:指定目标缓冲区对象。 符号常量必须是GL_ARRAY_BUFFER或GL_ELEMENT_ARRAY_BUFFER
offset:指定开始数据替换的缓冲区对象的数据存储区的偏移量，以字节为单位。
size:指定要替换的数据存储区域的大小（以字节为单位）。
data:指定将被复制到数据存储中的新数据的指针。

# glCheckFramebufferStatus

GLenum glCheckFramebufferStatus(GLenum target);

target:指定目标帧缓冲区对象，符号常量必须是GL_FRAMEBUFFER。

# glClear

void glClear(GLbitfield mask);

mask:指示要清除的缓冲区的掩码按位或，掩码是：GL_COLOR_BUFFER_BIT，GL_DEPTH_BUFFER_BIT和GL_STENCIL_BUFFER_BIT。

# glClearColor

void glClearColor(GLclampf red,GLclampf green,GLclampf blue,GLclampf alpha);

指定清楚颜色缓冲区时使用的RGBA值，初始值都是0；

# glClearDepthf

void glClearDepthf(GLclampf depth);

depth:指定深度缓冲区被清除时使用的深度值，初始值是1。

# glClearStencil

void glClearStencil(GLint s)


s:指定清除模板缓冲区时使用的索引。 初始值为0。

# glColorMask

void glColorMask(GLboolean red,GLboolean green,GLboolean blue,GLboolean alpha);

指定是否可以将红、绿、蓝和Alpha写入帧缓冲区。初始值都是GL_TRUE，表示可以写入颜色分量。

# glCompileShader

void glCompileShader(GLunit shader);

shader:指定要编译的着色器对象

# glCompressedTexImage2D 

void glCompressedTexImage2D( GLenum target,  GLint level,  GLenum internalformat,  GLsizei width,  GLsizei height,   GLint border,  GLsizei imageSize,   const GLvoid * data)

target:指定活动纹理单元的目标纹理，必须是GL_TEXTURE_2D，GL_TEXTURE_CUBE_MAP_POSITIVE_X，GL_TEXTURE_CUBE_MAP_NEGATIVE_X，GL_TEXTURE_CUBE_MAP_POSITIVE_Y，GL_TEXTURE_CUBE_MAP_NEGATIVE_Y，GL_TEXTURE_CUBE_MAP_POSITIVE_Z或GL_TEXTURE_CUBE_MAP_NEGATIVE_Z

level:指定详细程度，级别0是基本图像级别，级别n是第m个缩减映像

internalformat:存储在地址数据中的压缩图像数据的格式

width:指定纹理图像的宽度。所有实现都支持宽度至少为64 texels的2D纹理图像和宽度至少为16 texels的立方体贴图纹理图像

height:指定纹理图像的高度。所有实现都支持至少64像素高的2D纹理图像和至少16像素高的立方体贴图纹理图像

border:指定边框的宽度。必须为0

imageSize:指定从数据指定的地址开始的图像数据的无符号字节数

data:指定一个指向内存中压缩图像数据的指针

# glCompressedTexSubImage2D 

void glCompressedTexSubImage2D(GLenum target,
 	GLint level,
 	GLenum internalformat,
 	GLsizei width,
 	GLsizei height,
 	GLint border,
 	GLsizei imageSize,
 	const GLvoid * data);//指明一个二维的压缩纹理图像

target 指定活动纹理单元的目标纹理，必须为GL_TEXTURE_2D, GL_TEXTURE_CUBE_MAP_POSITIVE_X,GL_TEXTURE_CUBE_MAP_NEGATIVE_X, GL_TEXTURE_CUBE_MAP_POSITIVE_Y, GL_TEXTURE_CUBE_MAP_NEGATIVE_Y,GL_TEXTURE_CUBE_MAP_POSITIVE_Z,或者GL_TEXTURE_CUBE_MAP_NEGATIVE_Z.

level：指定细节级别数，0级表示基本图像级别，n级表示第n级mipmap缩小图。

internalformat 指定data中压缩图像数据的存储格式

width 指明纹理图像的宽度，所有OpenGL实现支持的2D纹理图像都至少为64纹素（texel）宽，立方体映射纹理图像都至少为16纹素宽。

height 指明纹理图像的高度，所有OpenGL实现支持的2D纹理图像都至少为64纹素（texel）高，立方体映射纹理图像都至少为16纹素高。

border 指定边框宽度，必须为零。

imageSize 指定data中压缩纹理图像的大小，单位为byte

data 指定一个指向压缩图像数据内存的指针。

# glCopyTeXImage2D

# glCopyTexSubImage2D

# glCreateProgram

GLunit glCreateProgram(void);创建程序对象

# glCreateShader

GLunit glCreateShader(GLenum shaderType);

shaderType:指定要创建的着色器的类型。 必须是GL_VERTEX_SHADER或GL_FRAGMENT_SHADER。

# glCullFace

void glCullFace(GLenum mode);

mode:指定正面或背面多边形是否为剔除的候选对象。符号常量GL_FRONT，GL_BACK和GL_FRONT_AND_BACK被接受。 初始值是GL_BACK。

# glDeleteBuffers

void glDeleteBuffers(GLsizei n, const GLunit * buffer);

n:指定要删除的缓冲区对象的数量

buffers:指定要删除的缓冲区对象的数组

# glDeleteFramebuffers

void glDeleteFramebuffers(GLsizei n, const GLunit * framebuffers);

n:指定要删除的帧缓冲区对象的数组

framebuffers:指定要删除的帧缓冲区对象的数组

# glDeleteProgram

void glDeleteProgram(GLunit program);

program: 指定要删除的程序对象

# glDeleteRenderbuffers

void glDeleteRenderbuffers(GLsizei n, const GLunit * render buffers);

n:指定要删除的渲染缓冲区对象的数量

renderbuffers:指定要删除渲染缓冲区对象的数组

# glDeleteShader

void GLDeleteShader(GLunit shader);

shader：指定要删除的着色器对象。

# glDeleteTexture

void glDeleteTexture(GLsizei n,const GLunit * textures);

n:指定要删除的纹理数量

textures:指定要删除的纹理数组

# glDepthFunc

void glDepthFunc(GLenum func)指定用于深度缓冲区比较的值;

func: 指定深度比较功能。常量：GL_NEVER，GL_LESS，GL_EQUAL，GL_LEQUAL，GL_GREATER，GL_NOTEQUAL，GL_GEQUAL和GL_ALWAYS。 初始值是GL_LESS。

# glDepthMask

void glDepthMask(GLboolean flag);

flag: 深度缓冲区是否可写入，GL_FALSE

# glDepthRangef

void glDepthRangef(GLclampf nearVal, GLclampf farVal);

nearVal:指定近剪裁平面到窗口坐标的映射。 初始值为0。

farVal:指定远裁剪平面到窗口坐标的映射。 初始值是1。

# glDetachShader

void glDetachShader(GLunit program,GLunit shader);

program: 指定要分离着色器对象的程序对象

shader:指定要分离的着色器对象

# glDisable

# glDisableVertexAttribArray

# glDrawArrays

void glDrawArrays(GLenum mode,GLint first,GLsizei count);

mode:指定要呈现哪种基元， 符号常量GL_POINTS，GL_LINE_STRIP，GL_LINE_LOOP，GL_LINES，GL_TRIANGLE_STRIP，GL_TRIANGLE_FAN和GL_TRIANGLES

first:指定已启用阵列中的起始索引

count:指定要呈现的索引数量

# glDrawElements

void glDrawElements(GLenum mode,GLsizei count,GLenum type,const GLvoid * indices);

mode:指定要呈现哪种基元。符号常量GL_POINTS，GL_LINE_STRIP，GL_LINE_LOOP，GL_LINES，GL_TRIANGLE_STRIP，GL_TRIANGLE_FAN和GL_TRIANGLES。

count:指定要呈现的元素数量

type:指定索引中值的类型

indices:指定一个指向索引存储位置的指针

# glEnable/与glDisable相反

void glEnable(GLenum cap);

cap：指定一个表示GL能力的符号常量。

# glEnableVertexAttribArray/与glDisableVertexAttribArray相反

void glEnableVertexAttribArray(GLunit index)

index:指定要启用的通用顶点属性的索引

# glFinish

void glFinish(void);

直到所有gl命令完成后才会返回该函数

# glFlush

void glFlush(void)；

在有限的时间内强制执行GL命令

# glFramebufferRenderbuffer

void glFramebufferRenderbuffer(GLenum target,GLenum attachment,GLenum renderbuffertarget,GLunit renderbuffer);

target:指定帧缓冲区目标，符号常量是：GL_FRAMEBUFFER。

attachment:指定渲染缓冲区应该附加到的连接点。必须是以下符号常量之一:GL_COLOR_ATTACHMENT0，GL_DEPTH_ATTACHMENT或GL_STENCIL_ATTACHMENT。

renderbuffertarget:指定渲染缓冲区目标，符号常量必须是GL_RENDERBUFFER。

renderbuffer:指定要附加的渲染缓冲区对象。

# glFramebufferTexture2D

void glFramebufferTexture2D(GLenum target,GLenum attachment,GLenum textarget,GLunit texture,GLint level);

target:指定帧缓冲区目标，符号常量是：GL_FRAMEBUFFER。

attachment:指定要从纹理贴图的连接点。GL_COLOR_ATTACHMENT0，GL_DEPTH_ATTACHMENT或GL_STENCIL_ATTACHMENT。

textarget:指定纹理目标。GL_TEXTURE_2D，GL_TEXTURE_CUBE_MAP_POSITIVE_X，GL_TEXTURE_CUBE_MAP_NEGATIVE_X，GL_TEXTURE_CUBE_MAP_POSITIVE_Y，GL_TEXTURE_CUBE_MAP_NEGATIVE_Y，GL_TEXTURE_CUBE_MAP_POSITIVE_Z或GL_TEXTURE_CUBE_MAP_NEGATIVE_Z。

texture:指定要附加图像的纹理对象

level:指定要附加的纹理图像的mipmap级别，该级别必须为0.

# glFrontFace

void glFrontFace(GLenum mode);

mode:指定前向多边形的方向。 GL_CW和GL_CCW, 初始值是GL_CCW。

# glGenBuffers

void glGenBuffers(GLsizei n,GLunit * buffers);

n:指定要生成的缓冲区对象名称的数量

buffers:指定存储生成的缓冲区对象名称的数组

# glGenerateMipMap

void glGenerateMipmap(GLenum target)

target:指定纹理对象绑定到的活动纹理单元的纹理目标，其中将生成mipmap。 必须是以下符号常量之一：GL_TEXTURE_2D或GL_TEXTURE_CUBE_MAP。

# glGenFramebuffers

void glGenFramebuffers(GLsizei n,GLunit * framebuffers);

n:指定要生成的帧缓冲区对象名称的数量

framebuffers：指定存储生成的帧缓冲区对象名称的数组

# glGenRenderbuffers

void GLGenRenderbuffers(Glsizei n,GLunit * renderbuffers)；

n:指定要生成的渲染缓冲区对象名称的数量

renderbuffers：指定存储生成的渲染缓冲区对象名称的数组

# glGenTextures

同上，针对纹理texture操作

# glGet

void glGetBooleanv(GLenum pname,GLboolean * params);

void glGetFloatV(GLenum pname,GLfloat * params);

void glGetIntegerv(GLenum pname,GLint * params);

pname:指定要返回的参数值————有一些常量参数，见网址

params:返回指定参数的一个或多个值

# glGetActiveAttrib

void glGetActiveAttrib(GLuint program,  
  GLuint index,  
  GLsizei bufSize,  
  GLsizei * length,  
  GLint * size,  
  GLenum * type,  
  GLchar * name); 

program:要查询的程序对象

index:要查询的属性变量的索引

bufsize:允许OpenGL写入名称指定的字符缓冲区的最大字符数

length:如果传递的不是NULL，则返回由OpenGL在名称指示的字符串中实际写入的字符数

size:返回属性变量的大小

type:返回属性变量的数据类型

name:返回包含属性变量名称的以空字符结尾的字符串。

# glGetActiveUniform

参考上一个函数，该函数针对的是Uniform变量（一致变量），注：与Attribute变量在颜色渲染中的区别

# glGetAttachedShaders

void glGetAttachedShaders(GLunit program,GLsizei maxCount,GLsizei * count,GLunit * shaders);

program:指定要查询的程序对象

maxCount：指定用于存储返回对象名称的数组大小

count：返回着色器中实际返回的名称数量

shaders：指定用于返回附加着色器对象名称的数组

# glGetAttribLocation

GLint GLGetAttribLocation(GLunit program,const GLchar * name):

program:要查询的程序对象

name:包含要查询其位置的属性变量的名称以空字符结尾的字符串

# GLGetBufferParameterteriv

void glGetBufferParameteriv(GLenum target,GLenum value,GLint * data);

target:目标缓冲区对象，GL_ARRAY_BUFFER或GL_ELEMENT_ARRAY_BUFFER。

value:缓冲区对象参数的符号名称。 接受的值是GL_BUFFER_SIZE或GL_BUFFER_USAGE。

data:返回请求的参数。

# glGetError

