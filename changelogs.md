Changelogs
===
### Modern UI 3.11.1.6
This is a Minecraft-only update, the Modern UI core does not change.  
**Modern UI** is likely to be renamed to **ModernUI** in the next version.
#### Forge Extension 1.20.1 / NeoForge Extension 1.20.1
* Suppress indirect crashes due to broken mod state
* Ignore translation-z for exact tooltip positioning
* Fix multiple tooltip colors not working
#### Fabric Extension 1.20.1
* Improve modern tooltip compatibility on Fabric
* Add config for tooltip line wrapping on Fabric
* Others are functionally equivalent to Forge version
#### Modern Text Engine 1.20.1
* Fix the compatibility with polytone
* Fix text effect of color emoji is always white
* Exclude CozyUI fonts by default
* Remove duplicates when dumping bitmap fonts
* Use isLenient for parsing font definition files
* Fix large bitmap fonts being ignored

### Modern UI 3.11.1.1
#### Forge Extension 1.20.1 / NeoForge Extension 1.20.1
* Add ExtendedGuiGraphics that allows other mods to draw rounded rectangles in vanilla-based GUI
* Add emoji shortcode suggestions
* Fix lifecycle bug, improve UI slider
* Fix tooltip title break not showing up on certain GPUs
* Update to Emoji 16.0
* Fix startup crash on dedicated server
* Fix crash in PojavLauncher
* Some other fixes, improvements and optimizations
#### Fabric Extension 1.20.1
* Fix game loading complete sound "DING" not working in some cases
* Others are functionally equivalent to Forge version
#### Modern Text Engine 1.20.1
* Improve experience level rendering
* Optimize white texture and text effect rendering
* No longer register fonts in minecraft namespace
  - Use `"font":"modernui:jetbrains-mono-medium"` to change font
* Set max allowed value for minPixelDensityForSDF to 10
* Use point sampling for A8 atlas by default as an optimization
  - We prefer computeDeviceFontSize and allowSDFTextIn2D, if some mods use `RenderSystem.getModelViewMatrix()` to
    scale, or either of the above two options is false, or Shaders are active, you can set linearSamplingA8Atlas to
    true to get better quality
* Align text shadow to pixel grid to improve rendering, change default shadow offset to 0.5
* Further improve text rendering quality at any scale (such as for Mekanism, JourneyMap), you can disable this
  by setting computeDeviceFontSize to false
* Rework obfuscated char rendering, improve quality, balance performance and compatibility
* Fix a bug in handling hover and click events with styleAtWidth() (which can cause single char after SPACE char
  not clickable)
* Fix font index is not unsigned during layout
* Always create 256x256 font texture for bitmap font when using dedicated texture
* Use 32-bit int for bearing X and bearing Y, allow large metrics for bitmap fonts
#### Core Framework
* Allow to use MENU key to open/close context menu
* Add option to create mutable Bitmap from encoded data
* Add method to explicitly release Shader
* Add method to clear a rectangle of Bitmap to some color
* Add a number of methods to access/convert pixels in bulk
* Add Bitmap.getColor4f() and Bitmap.setColor4f() to access pixel value at high precision
* Add Bitmap.setFormat() and Bitmap.setPremultiplied() to reinterpret existing pixel data with a new type
* Add a large number of pixel formats for Bitmap, and add methods for converting between different pixel formats,
  these new formats can also be used to create textures
* Add density for Image, allowing it to be scaled in ImageDrawable/ImageView/ImageSpan
* Replace some copy-on-read list with copy-on-write list
* Disable default scroll bar for AbsListView
* Not force skipping OpenGL error checks, always print GLCaps
* Add fallback method to compute font metrics
* Add method to create Bitmap by wrapping an existing address
* Remove dimension restriction on Bitmap creation
* Temporarily fix lifecycle never reaches RESUME state
* Many other optimizations and internal changes
#### Core Framework - Kotlin Extension
* No changes
#### Markdown Extension
* No changes
#### Arc3D Graphics Engine
* Change Shader and ColorFilter to sealed interface (and RefCounted)
* Add Pixmap.clear() to clear a rectangle of pixels
* Add low precision pixel load function
* Add half float support
* Add 16-bit per channel pixel format conversion
* Optimize pixel ops and loops
* Refactor color types and optimize pixel format conversion
* Rename rowStride to rowBytes, limit rowBytes to Int32.Max
* Add method for access/convert pixels in bulk
* Engine
  - Update the initialization of image format capabilities
  - Improve caps dump
  - Add named methods to Swizzle
* OpenGL backend
  - Workaround Intel driver bug that causes rendering broken
  - Improve GLCaps initialization
  - Some other internal changes
* Shader Compiler
  - Add initializer list grammar
  - Add vertex_id and instance_id builtin for OpenGL
  - Update SPIR-V generator for sampler operations
  - Add array stride decoration for all supported types for type matching
  - Update descriptor set validation
  - Initially add switch statement parsing
  - Tons of updates on SPIR-V code generator, SPIR-V generation is now basically functional,
    but not yet used in production
  - Add struct declaration grammar
  - Add scoped block grammar
* Granite Renderer
  - Add workaround when there is no clamp_to_border support
  - Split up universal blend shader snippet
* Vulkan backend
  - Add full method to create VulkanImage
  - Refactor some class structures
  - Add VulkanImageView
  - Add VulkanMemoryAllocator to allocate memory for images/buffers
  - Some other internal changes
* Some other internal changes

### Modern UI 3.11.0.1
#### Forge Extension 1.20.1 / NeoForge Extension 1.20.1
* Add MinecraftSurfaceView to handle raw rendering calls
* Ensure that all (native/GPU) resources are closed when the game exits
* Slightly improve the Center UI
* Fix a random crash when opening/closing UI frequently
* Rework tooltip rendering
  - Add white noise to shadow
  - Add dithering to gradient colors
  - Use L1 norm instead of L2 norm for coverage antialiasing
  - Change shadow approximation method
  - Change default border radius and shadow alpha
  - Add new conditions for adding the extra space below tooltip title line
  - If the first three lines of the tooltip have different styles, we consider the first line as the title
  - Reduce the saturation of default tooltip colors
* Allow using arrow keys to manually scroll the tooltip
* Add small epsilon to text Z value for tooltip rendering to work around FP errors on some GPUs
* Optimize blur effect
  - Use texelFetch instead of texture
  - Remove the additional blit pass and render target because we work around a Minecraft bug
  - Try to cache the shader program and temporary render target for blurring, and handle errors
  - Apply blur effect to the screen background instead of the world, just like Minecraft 1.20.6
* Migrate to new rendering pipeline
#### Fabric Extension 1.20.1
* Add support for Minecraft 1.20
* Fix key binding not working in some cases
* Others are functionally equivalent to Forge version
#### Modern Text Engine 1.20.1
* Add compatibility for bitmap fonts with custom text shader
* Enable linear metrics and disable font hinting by default
* Add config to change the minimum pixel density for SDF text
* Fix some possible bugs on text rendering
* Optimize text rendering
  - Add texture cleanup to FontResourceManager
  - Simplify text layout rendering code
  - Use Math.round for aligning pixels
  - Fix glyph info for FontSet compatibility
* Rework and optimize bitmap font rendering
  - Try to stitch bitmap font into atlas
  - Try to discard bitmap fonts if they have negative metrics, transparent pixels, or huge metrics
  - Saturate glyph metrics for bitmap font
  - Fix hashCode and equals for correct de-duplication
* Adjust lod bias for normal text shader
* Adjust bitmap font to match vanilla behavior
  - Adjust glyph advance calculation
* Adjust Unicode font loading behavior
  - Any reference to vanilla Unicode font and UNIHEX font will redirect to current ModernUI default typeface list
    instead of system fonts, except for Minecraft default font set
* Fix text layout bug when finding style transitions
* Allow caching the missing glyph to atlas
* Adopt full text rendering technology from core framework
* Fix line breaker that may output no lines and keep consistency with vanilla behavior
  - This fix a bug with IBE Editor
* Fix text strike cache invalidation for FontSet compatibility
  - This fix a bug with Create
* Add text layout dump in advanced options
* Add a command for debugging line breaker
* Add methods for debugging text engine
#### Core Framework
* Enable linear text by default, increase layout cache limit
* Delete render thread executor
* Delete old text rendering code
* Add GradientDrawable that draw shapes with gradient colors
* Update/fix ShapeDrawable with latest rendering pipeline
* Add set/get ColorFilter to Drawable and ImageView Add ImageView.setImageTintBlendMode
* Rework ImageDrawable.setSrcRect() method
* Update ImageDrawable with antialias, dither, filter, and tile modes
* Add setter/getter to change blend mode for edge effect
* Change default blend mode for EdgeEffect from SRC_OVER to SRC_ATOP
* Fix Matrix.mapRect()
* Fix EdgeEffect centerX
* Improve text rendering
* Add AngularGradient API and implementation
* Add RadialGradient API and implementation
* Add LinearGradient API and implementation
* Add GradientShader API and implementation
* Add new draw methods to Canvas class
* Add BlendModeColorFilter and make it work finally, default blend mode for ImageDrawable is SRC_IN
* Add ColorFilter class that can be installed on Paint
* Refactor Image class and fix Image.close() issue
* Refactor Paint class
* Add ImageShader class
* Add Shader class that can be installed on Paint
* Add TextView.setTextSize() that specifies a unit, default is sp
* Full migration to the new rendering pipeline, Arc3D Granite Renderer; delete old GLSurfaceCanvas
* Avoid re-layout on window minimized, since framebuffer is destroyed and size is 0
* Deprecate Canvas.saveLayer() for future layer compositor and render tree
#### Core Framework - Kotlin Extension
* No changes
#### Markdown Extension
* No changes
#### Arc3D Graphics Engine
* Remove old usage of Image.getSurfaceFlags
* Add Image.getUniqueID() and static methods to create raster images
* Add utility NoDrawCanvas NWayCanvas and PaintFilterCanvas
* Fix Matrix.mapRect() is not correct
* Fix compiler error
* Optimize text ops if subRunToDevice is translation-only and pipeline does not require local coords trivially
* Optimize matrix computation for text ops
* Replace Matrix4 in rendering code with Matrix
* Make Matrix4() construct an identity matrix, and Matrix4.identity() return a read-only identity matrix
* Fix TextBlobBuilder offsets not reset after build
* Add RoundRect flatten methods
* Improve NoPixelsDevice clip tracking, remove ConservativeClip
* Add DrawAtlas.purge() to free unused pages
* Add implementation for gradients in other interpolation color spaces and for all hue interpolation methods
* Allow DrawAtlas to perform an immediate compact
* Rename some classes and methods
* Change the default uniform buffer block size to 32KB
* Fix color array copy in Vertices::makeCopy
* Fix persistent mapping check in GLBuffer
* Temporarily enable RGB texture in OpenGL
* Try to share vertex array objects in OpenGL backend
* Expose resource cleanup API, also cleanup framebuffer cache and strike cache
* Review ResourceCache, fix some legacy issues
* Add support for alpha-only images, add missing Shaders shader implementation
* Purge framebuffers immediately after one attachment was destroyed
* Complete the compatibility with OpenGL 3.3 and OpenGL ES 3.0
* Improve texture and renderbuffer creation
* Deprecate old Device methods
* Fix OpenGL 3.3 and GLSL 330 compatibility
* Finalize BoundsManager, add samples
* Add plus_clamped, minus, and minus_clamped blend info
* Remove 01 coverage in non-aa case
* Add blend equation in GL backend
* Mark old code as deprecated
* Implement basic functionality for final blender, enable dual source blending
* Fully implement BakedTextBlob and TextBlobCache for text rendering
* Fix blend shader doesn't compile
* Add TextBlob as an immutable container for glyph rendering
* Rework FramebufferDesc, add FramebufferCache to manage framebuffers
* Basically implement texture copy task, implement Surface.onNewImageSnapshot()
* Add factory method to create Surface
* Implement Device management
* Invalidate atlases if RC.snap() failed
* Fix several threading issues for OpenGL backend
* Handle ColorFilter properly
* Add BlendModeShader
* Fix color space transformation on paint's solid color
* Add primitive color blending and color space transform
* Add blending with shader and paint's alpha
* Fix color space transformation on BlendModeColorFilter
* Add implementation of BlendModeShader and BlendModeColorFilter
* Remove Geometry interface
* Add Vertices class and Vertices step to drawVertices
* Add shader implementation for 42 blend modes
* Fix arg name for uniforms that start with no mangle prefix
* Add StaticBufferManager and Buffer-to-Buffer copy task
* Fix ImageUploadTask bug
* Implement remaining important Canvas methods
* Add and implement new Canvas methods in Device
* Fix depth is perspective-correct; the depth should be preserved, then multiply it by w.
* Fix bugs on arc shader with square end
* Finish methods to create and draw GlyphRuns
* Add method to set Matrix elements
* Fix Matrix4.hashCode() for negative zero
* Add Geometry.getBounds() to compute bounds
* Improve ClipStack to compute several bounds
* Fix stroke inflation radius computation for inner and outer stroke
* Optimize draw when it does not depend on dst
* Fix several issues on Device
* Implement the creation of AtlasSubRuns
* Add method to compute res scales if matrix has perspective
* Fix AnalyticSimpleBoxStep instance data type
* Add method to draw pie and chord, optimize shaders
* Add rendering with three cap types of stroke arcs initially
* Implement Atlas text op at low level, improve solid color fast path, trying to handle primitive color
* Fix ScalerContext_JDK does not return a reliable glyph bounds
* Fix DrawAtlas assertion and GlyphAtlasManager row stride
* Fix Strike and ScalerContext bugs, remove stroke cap in StrikeDesc
* Improve finite check and non-invertible matrix
* Add RendererProvider to manage GeometryRenderers
* Finish implementation of atlas management for draw ops and glyph atlas
* Calculate the Path byte size when generating Glyph in Strike
* Implement Strike, StrikeCache, and ScalerContext basically
* Add Paint.setPathEffect(), add missing javadoc in Font
* Add Path.transform(), add PathIterator.getFillRule()
* Add GPU dithering implementation (no texture lookup)
* Fix GLCaps.FormatInfo for RGB565
* Update Paint and related classes
* Make Blender and ColorFilter strictly ref-counted
* Add Shader.isConstant()
* Fix Canvas.drawCircle()
* Add Paint.setColor4f()
* Fix Paint.setStrokeWidth() and Paint.setStrokeMiter() for NaN values
* Remove Paint's SmoothWidth, MaskFilter and ImageFilter
* Add PathEffect skeleton class
* Fix several hashCode implementation for negative zeros
* Update Paint.nothingToDraw() for more blend modes
* Add more methods to RoundRect
* Update Surface, Canvas, and related classes
* Add Stroke, PathIterable, update PathStroker
* Optimize shaders
* Use short-circuit for transfer function
* Use texelFetch for cubic shader, remove invImageSize uniform
* Add perspective correction for local matrix shader
* Extract color space transform from image shaders
* Ensure subset sampling does not use mipmaps
* Implement bicubic and strict subset sampling
* Change AnalyticSimpleBoxStep to use L1 norm
* Fix bug on GLImageDesc.equals()
* Fix bug on uniform block layout
* Change Paint constants and SamplingOptions, adding classes for text rendering
* Done depth stencil work, fix several bugs
* Add flipY and unorm clamp for PixelUtils
* Implement LinearGradient, RadialGradient, AngularGradient
* Fix bugs on ImageShader.makeSubset()
* Fix bugs on premul & unpremul in some classes
* Improve ColorSpace transform, add PixelUtils.convertPixels()
* Add new ColorSpace transform shader
* Fix GLSampler TEXTURE_WRAP_R is not set, add validation for SamplerDesc
* Fix Matrix4.invert, add Matrix.toMatrix4, fix UniformDataGatherer for mat3
* Make Paint, PaintParams, and Draw classes closeable
* Fix TextureTracker; rename gradient shaders
* Optimize box shader
* Accumulated updates on fragment effects and shading pipeline
* Implement simple pixel upload using image-to-image copy
* Add new Shader and ColorFilter classes
* Rename PixelMap to Pixmap, PixelRef to Pixels
* Switch slow JNI to PixelUtils.copyImage() for array to off-heap copy
* Remove the offset parameter of Buffer.unmap()
* Finish AnalyticSimpleBoxStep
* Allow implicit conversion between numerics
* Add DepthStencilSettings and BoundsManager, limit the number of geometry steps
* Optimize vertex writer and uniform writer, optimize uniform data deduplication
* Basically complete the Granite Renderer
* Add geometry projection, solid color simplification
* Finish RenderPassTask execution Fix scissor origin, initial scissor setup
* Complete DrawPass's texture sampler binding
* Add TextureDataGatherer, texture sampler binding and tracker
* Add UniformDataGatherer and UniformDataCache
* Fix Matrix4.store()
* Add framebuffer creation and some tests
* Some work on new PipelineBuilder
* Update Buffer, GLBuffer, persistent mapping and so on
* Accumulative updates for new renderer
* Add method for updating clip draws
* Update ClipStack
* Improve vertex specification and buffer binding
* Rename the project from 'Arc 3D' to 'Arc3D'
* Commit all accumulative updates
* Change BlendMode.apply() to static methods
* Accumulative updates for the new pipeline
* Attempt to refactor pipeline
* Add more classes for new pipeline
* Add frexp & ldexp impl
* Some attempts on pipeline
* Refactor GPU Image, RenderTarget, SurfaceProxy classes; remove Texture
* Add Image and Framebuffer creation, add reusable framebuffers
* Refactor GpuResource class hierarchy
* Support GL_CONTEXT_LOST
* Tons of work on Engine and OpenGL backend, not listed
* Add pre-defined extensions to compile options
* A lot of work on abstraction between GL3 and GLES3
* Initially add GLInterface for both OpenGL & OpenGL ES support
* Add std140/std430 layout qualifiers, add include directive parsing
* Abandon usage of GLSL ARB extensions that core in later versions
* Fix GLCaps crash for some capabilities
* Fix some bugs in preprocessing
* Other improvements
* Add new preprocessing methods, allow sub-range source
* Add StringLiteral grammar, fix Whitespace grammar
* Add FatalError to terminate compiler
* Add identifier name length check (1024 at most)
* Add benchmark between Arc3D and shaderc (glslang)
* Update Lexer
* Add directive grammar
* Add 'using' grammar for type aliases
* Add newline token, fix block comment grammar

### Modern UI 3.10.1.4
#### Forge Extension 1.20.1 / NeoForge Extension 1.20.1
* Do not use new word breaker in command mode
* Add preferences navigation to mods config button
* Improve PreferencesFragment
* Add API to allow back to previous screen, allow passing a ScreenCallback
* Add API to create MuiScreen
* Add Segoe UI Symbol to default fallback list
* Fix issue with TrueType Collection registration
* Add font registration config to register additional fonts
* Add modifiers to ACTION_SCROLL event
* Add showing layout bounds
* Add adaptive tooltip colors
* Renew tooltip rendering
  - Create rendertype_modern_tooltip shader
  - Interpolate color bilinearly in sRGB space
  - Better shadow effect, add shadow opacity
  - Add corner radius config
  - Adjust auto scrolling velocity
  - Fix bugs on exact positioning with some mods
* Fix a rare crash on config reloading due to thread-safety
* Apply blur effect only to screens that have default background (configurable)
* Do not use Overwrite for calculateScale
* Fix startup crash on server and datagen
* Remove ScreenCallback capability
* Refactor project structure and bootstrap
#### Fabric Extension 1.20.1
* Fix tooltip compatibility with Sodium
* Others are functionally equivalent to Forge version
#### Modern Text Engine 1.20.1
* Change logging level for font loading, enhance onFontRegistered thread-safety
* Add new default font behaviors and rule set, allowing regexes to match fonts
* Adjust text renderer alpha threshold from 1 to 2 (0-255)
* Fix only a very small set of characters can be used for obfuscated rendering
* Use Latin1 for FastCharSet
* Fix a rare crash on text engine due to batch rendering and display mode changes
#### Core Framework 3.10.1
* Update typecast checks, add ArrayMap.forEach
* Make FontFamily.createFamily throw Exception
* Add FontFamily.createFamilies for TrueType Collection
* Add HorizontalScrollView, update ScrollView
* Add debug layout to show layout bounds
* Optimize Color.parseColor
* Add Animatable and Animatable2
* Add some missing javadoc
* Use UTF-16 for TextUtils read/write
* Add TextPaint.baselineShift and Subscript/SuperscriptSpan
* Disable pooling of Message objects
* Build against a copy of Arc3D, instead of composite build
* Add Canvas.shear / skew, deprecate Canvas.getMatrix
* Add TextUtils.concat and TextUtils.join methods
* Make use of Java 20 float/half convert instruction
* Add CharBuffer support for TextUtils.getChars()
#### Core Framework - Kotlin Extension 3.10.1
* No changes
#### Markdown 3.10.1
* No changes
#### Arc 3D Graphics Engine 3.10.1
* Add 3D shearing transform methods
* Improve GL_TEXTURE_SWIZZLE_RGBA compatibility
* Tons of updates on DSL shader compiler, including new grammar parsing and SPIR-V generation, no detailed information provided

### Modern UI 3.10.0.4
#### Forge Extension 1.20.1 / NeoForge Extension 1.20.1
* Add Markdown preview
* Use vanilla border style for modern tooltip (when rounded = false)
* Add font names for registered fonts, add JetBrains Mono
* Update to Emoji 15.1
* Add auto scroll when tooltip is out of screen
* Add shadow effect for tooltip
* Add developer mode config to Preferences GUI
* Hide Advanced Options and Dev when not in developer mode
* Adjust default font behavior to be locale-sensitive
* Tweak fallback font loading behavior (now it accepts font files)
* Move destroy() method so that the game won't crash in forced tick after the window closes
* Handle glowing sign where text color is black
* Update Traditional Chinese - notlin4
#### Fabric Extension 1.20.1
* Enhance tooltip compatibility with Sodium (when rounded = false)
* Add tooltip line wrapping for Fabric
* Add tooltip center title and title break for Fabric
* Others are functionally equivalent to Forge version
#### Modern Text Engine 1.20.1
* Add Untranslated Items integration
* Fix useComponentCache not working at all
* Fix force unicode font not working after game restart
* Fix line breaker SIOOBE for illegal string (this fixed crash with Better Statistics Screen)
#### Core Framework 3.10.0
* Move kotlin extension to a separate module (Core-KTX)
* Add Log class to avoid using log4j in submodules
* Implement blend mode filter for ShapeDrawable, ColorDrawable and other Drawable classes
* Fix incorrect drop-down position in RTL layout direction
* Fix MenuPopup overlap anchor (google-bug) (fix #199)
* Fix TextShaper context range for BiDi analysis
* Add LocaleSpan
* Add all 42 blend modes that used in Photoshop (currently no shader implementation)
* Update BlendMode and Color.blend()
* Change Bitmap.getSize() type to long
* Make Bitmap's color info mutable (for reinterpretation)
* Add path measurement implementation (PathMeasure class)
* Remove 2GB restriction on Bitmap creation, add more sanitizations
* Deprecate ImageStore, fix javadoc errors
* Update Bitmap with Arc3D
* Update Matrix and Path with Arc3D
* Fix Underline and Strikethrough offset
* Add "exclusive" East Asian family support (currently not used)
* Public Menu.setOptionalIconsVisible() method
* Change atlas coverage type to double
#### Core Framework - Kotlin Extension 3.10.0
* Add kotlin-flavored methods, update annotations
#### Markdown 3.10.0
* Suppress unchecked warning
#### Arc 3D Graphics Engine 3.10.0
* Add color filters and color matrix
* Add/update all blend modes and their raster implementations: PLUS, MINUS, DIFFERENCE, EXCLUSION, COLOR_DODGE, COLOR_BURN, HARD_LIGHT, SOFT_LIGHT, LINEAR_DODGE, LINEAR_BURN, VIVID_LIGHT, LINEAR_LIGHT, PIN_LIGHT, HARD_MIX and HSL blend modes (HUE, SATURATION, COLOR, LUMINOSITY)
* Rename shaderc package to compiler
* Add Image-derived and Shader-derived skeleton classes
* Add UNORM_PACK16 and UNORM_PACK32 encoding constant
* Public ColorType.channelFlags
* Add missing GRAY_ALPHA_88 for ColorType.encoding
* Add alpha type validation
* Make owner's reference to pixel map mutable
* Fix ColorSpace initializer
* Add Raster, remove heap version of Bitmap
* Add full path measurement implementation
* Add PixelUtils for pixel conversion
* Add PixelMap and PixelRef, remove Pixmap
* Add and optimize Path methods
* Add Path.bounds computation, optimize Path allocation
* Add Rect2fc and Rect2ic for read-only usage
* Inline Path.Ref usage count implementation
* Finish approximation of cubic strokes by quadratic splines
* Finish approximation of quadratic strokes by quadratic splines
* Add MathUtil.pin() method for capturing NaN values, replace some use of clamp()
* Add conic section to quadratic curves conversion
* Add several methods to reset the Path
* Finish RoundJoiner, fix Path reversePop
* Add Matrixc interface for read-only usage of Matrix
* Update and optimize PathStroker
* Optimize approximation of conic sections by quadratic splines
* Add PathConsumer
* Add Path tessellation for quadratic and cubic splines
* Add PathUtils and WangsFormula for subdivisions
* Add Path, add Path.Ref, add PathIterator
* Add Geometry class for finding inflection points, tangent, curvature, max curvature, cusp, solving quadratic equations, cubic equations, etc
* Add RefCounted interface
* Add Hardware transfer processor
* Optimize rectangle packer

### Modern UI 3.9.0.4
#### Forge Extension 1.20.1 / NeoForge Extension 1.20.1
* Fix validation errors
* Add font atlas compact
* Add Iris shaders integration
* Schedule GUI Scale value listener on next tick
* Better text config category
* Change typeface loading behavior
* Restore cursor position for Emoji shortcode substitution
* Rework font manager to implement core Emoji rendering
* Add GPU driver bug workarounds bootstrap properties
* Improve text field undo/redo
* Add undo/redo for EditBox
* Add GUI Scale to Preferences
* Add batch input commit
* Update translations
* Implement grapheme break for all text fields
* Implement break iter for vanilla EditBox
* Add music player
* Increase window size for OpenGL version test, fix game freeze on Linux
* Update font resources and licenses
* Add tooltip border width config
* Fix format error when setting color opacity
* Remove unused assets
* Completely switch to Arc3D and abandon GL*Compat
* Auto clean up less used GPU resources
* Always generate text config
* Use jar-in-jar for caffeine and flexmark
* Update synchronization, improve render performance
* Disable MSAA by default, 0.176x VRAM usage than before, and faster
* Update to latest Arc3D and ModernUI
#### Fabric Extension 1.20.1 / Quilt Extension 1.20.1
* Add GUI Scale slider for Fabric
* Fix mod logo on Fabric
* Others are functionally equivalent to Forge version
### Modern Text Engine 1.20.1
* Auto disable modern text shaders when Iris shaders are active
* Now follow vanilla's Force Unicode Font setting
* Fix compat with Loot Beams
* Fix compat with Debugify
* Fix compat with Curios
* Fix shadow offset Y for bitmap font
* Fix fist line rendering in sign edit GUI
* Add text layout command
* Remove text cache cleanup on parallel dispatch
* Dont draw text outline when 'modern text shaders in 3D' disabled
* Keep text shader preload consistent with vanilla UI shader preload
* Improve UniformScale text when GUI scale is less than 4

### Modern UI 3.8.2.4
#### Forge Extension 1.20.1-47.0.14 / NeoForge Extension 1.20.1-47.1.4
* Change the crash with TipTheScales to warning
* Remove bitwise AND in shaders
#### Fabric Extension 1.20.1-0.14.21-0.87.0 / Quilt Extension 1.20.1-7.1.2-0.87.0
* Remove bitwise AND in shaders
* Functionally equivalent to Forge version but removed some features
### Modern Text Engine 1.20.1
* Only override Font's StringSplitter

### Modern UI 3.8.1.5
#### Forge Extension 1.20.1-47.0.14 / NeoForge Extension 1.20.1-47.1.4
* Re-architect for platform abstraction
* Change step size for master volume multiplier option to 0.01
* Prevent Action Center from being opened when a screen with shouldCloseOnEsc=false is opened
* Request window attention when "Ding" is enabled
#### Fabric Extension 1.20.1-0.14.21-0.87.0 / Quilt Extension 1.20.1-7.1.2-0.87.0
* Functionally equivalent to Forge version but removed some features
#### Modern Text Engine 1.20.1
* No change

### Modern UI 3.8.1.4
#### Forge Extension 1.20.1-47.0.14
* Add OptiFine-like zoom
* Add master volume multiplier on window blur or minimized
* Add framerate limit on window blur or minimized
* Add hot reload of the default typeface list
* Add font selection list and open file dialog
* Separate old font family config into preferred one and fallbacks
* Fix ASCII digit input in Arabic
* Add tooltip center alignment
* Add tooltip title break
* Improve extra spacing below tooltip title
* Add config to switch between rounded rect or normal rect for tooltip border
* Add config for exact tooltip positioning
* Add maximized borderless mode
* Improve fullscreen borderless on Windows
* Update default config
* Fix crash on setting opacity to 0
* Fix possible crash in parsing color string
* Add Fragments into crash report
* Add more advanced options
#### Modern Text Engine 1.20.1
* Add fake italic support for bitmap fonts
* Add device font size computation in 2D
* Add SDF text control in 2D
* Add cache lifespan config back
* Optimize cache performance
* Add config for async text layout
* Fix text engine not fully disabled
* Fix memory leakage when reloading resources
* Add smart SDF text control
* Fix polygon offset issues
* Fix possible crash on populateDefaultFonts
* Add line break style config
* Add line break word style config
* Fix shadow offset for bitmap fonts
* Add redirect of UniformFont

### Modern UI 3.8.0.4
#### Forge Extension 1.20.1-47.0.14
* Add tooltips for some options
* Add in-game option for background opacity
* Use bootstrap.properties instead of bootstrap file
* Add dynamic tooltip border colors and presets
* Block NUL char for input method
#### Modern Text Engine 1.20.1
* Add config to control component cache
* Add default font behavior to control whether to use default font
* Add SpaceFont for compatibility
* Add position alignment for direct mask drawing
* Add StandardFontSet for better mod compatibility
* Make color emoji work in font itemization rather than brute force
* Enhance and optimize text layout engine
  * Only compute the required information
  * Make text layout asynchronous
  * Mix layout processor into LayoutCore to increase cache hit
  * Adjust paragraph layout lifespan
  * Reduce performance and memory impact
* Remove fast digit replacement
* Make obfuscated style work with bitmap fonts
* Adjust EditBox highlight color

### Modern UI 3.7.1.3 (2023-07-09)
#### Forge Extension 1.20.1-47.0.14
* Fix crash on dedicated server
* Fix possible startup crash
* Add ContainerDrawHelper
#### Modern Text Engine 1.20.1
* Fix EditBox selection highlight
* Fix per-glyph rendering for compatibility
* Fix obfuscated text crash in world using SDF

### Modern UI 3.7.0.5 (2023-06-21)
#### Forge Extension 1.20.1-47.0.14
* Port to 1.20
#### Modern Text Engine 1.20.1
* Port to 1.20

### Modern UI 3.7.0.2 (2023-06-20)
#### Forge Extension 1.19.4-45.1.0
* Add config to use vanilla font for convenience
* Remove tooltip fade-in animation
* Port to 1.19.4
* Add slider control for preferences
* Fix UI screenshot not un-premultiplied
* Don't allow soft launching due to OpenGL 3.3 support
* Fix GUI scale pinned after game restart
* Add CenterFragment2
* Remove noise from gaussian blur shader
* Remove deprecated configs
#### Modern Text Engine 1.19.4
* Make SDF work as long as in 3D or non-translation matrix
* Make SDF work with 32pt font size at least
* Remove alignPixels due to font hinting
* Replace 8x outline with SDF stroke
* Fix compatibility for Create display board
* Change Twemoji 14 to Google Noto Color Emoji 15
* Fix text rendered as emoji without VS-16 (0xFE0F)
* Combine IamCal (Slack) shortcodes with JoyPixels (Discord) and Google

### Modern UI 3.6.3.117 (2022-12-15)
#### Forge Extension 1.19.2-43.1.2
* Adjust GUI scale algorithm
* Adjust tooltip border width
#### Modern Text Engine 1.19.2
* Add distance field text to 3D world
* Fix total advance of layout is never pixel-aligned
* Fix TTF loading in vanilla resource packs
* Adjust texture sharpening factor
#### Core Framework 3.6
* Fix distance-to-edge anti-aliasing is gamma correct

### Modern UI 3.6.2.116 (2022-11-30)
#### Forge Extension 1.19.2-43.1.2
* Support capability for fragments and screens
* Fix incorrect color blending for tooltip
* Fix GUI scale is always auto after restart
* Fix black screen with blur effect
* Add glow wave effect
#### Modern Text Engine 1.19.2
* Fix line breaking for obfuscated chars
* Remove enchantment font hack
* Support vanilla bitmap font in replacement run
* Support vanilla bitmap font as font family
* Support vanilla font declaration
* Adjust text decoration thickness
* Reduce unnecessary native memory usage in vanilla
* Make font resource reloading work async
* Optimize ChatFormatting.getByCode to O(1)
* Optimize layout caching strategy
* Add font set to layout key
#### Core Framework 3.6
* Adjust analytic anti-aliasing to screen-space
* Improve font collection itemization
* Update shaders to a modern version

### Modern UI 3.6.1.115 (2022-10-07)
#### Forge Extension 1.19.2-43.1.2
* Change the background blur from 4-pass box blur to 2-pass gaussian blur with lod and noise
* Improve config reloading and action center UI
* Fix crash on dedicated server (though you shouldn't install on server)
* Add config to disable slider GUI scale
* Update GUI scale algorithm
#### Modern Text Engine 1.19.2
* Add sharpen font atlases
* Change blend mode for glowing text
#### Core Framework 3.6
* Use indexed rendering for glyph meshes
* Add sharpen textures for all shaders
* Always use premultiplied alpha for builtin renderer

### Modern UI 3.6.0.114 (2022-09-07)
#### Forge Extension 1.19.2-43.1.2
* Add I18n compat characters
* Add new API and remove server dependency
* Change registration and network to internal
* Support for OptiFine 1.19.2
* Migrate to MC & Forge 1.19.2
#### Modern Text Engine 1.19.2
* Add new glowing text effect
* Add deferred rendering to improve performance
* Migrate to MC 1.19.2
#### Core Framework 3.6
* Compact font atlas generation

### Modern UI 3.5.4.113 (2022-08-19)
#### Forge Extension 1.18.2-40.0.12
* Add support for creating window with the highest OpenGL it can
* Fix config reloading even if nothing changed
* Add debug stuff
#### Modern Text Engine 1.18.2
* No updates
#### Core Framework 3.5
* Workaround SPACE tunneling event is not consumed in EditText

### Modern UI 3.5.3.112 (2022-08-17)
#### Forge Extension 1.18.2-40.0.12
* Enhance GL caps error screen
* Add support for requesting OpenGL 4.6 or 4.5 core profile window avoiding GL caps errors
#### Modern Text Engine 1.18.2
* No updates
#### Core Framework 3.5
* Internal changes

### Modern UI 3.5.2.111 (2022-07-27)
#### Forge Extension 1.18.2-40.0.12
* Add debug stuff
* Add traditional Chinese support
#### Modern Text Engine 1.18.2
* Add support for sign glowing text
* Add shadow offset and outline offset config
* Fix auto disable OptiFine fast render not working
* Add support for COMBINING ENCLOSING KEYCAP
* Fix index crash when EditBox contains formatting codes
#### Core Framework 3.5
* Internal changes

### Modern UI 3.5.1.110 (2022-07-20)
#### Forge Extension 1.18.2-40.0.12
* Fix window mode sometimes didn't work correctly
* Fix tooltip BG or FG transparency sorting and write into depth buffer
#### Modern Text Engine 1.18.2
* Enhance and smooth EditBox rendering
* Adjust alpha threshold from 1 to 2
* Fix NPE when font renders fast chars nothing
* Fix line feed ignored when using fast path of line breaking
* Fix text empty when using fast path of text breaking backwards
#### Core Framework 3.5
* Internal changes

### Modern UI 3.5.0.109 (2022-07-12)
#### Forge Extension 1.18.2-40.0.12
* Make extensions backward compatible to OpenGL 3.3
* Add window mode config (like fullscreen borderless)
* Add config of ignoring GL errors
* Add GL error GUI and link directing
* Add right-to-left layout for modern tooltips
* Add in-game GUI for all new configs
* Add dump of memory info of all textures
* Fix tooltip shaking when rendering at bottom
* Dispatch generic pointer events
* Enable more configs to take effect in real-time without restarting
* Disable Minecraft render thread assertions
* Auto disable OptiFine fast render
#### Modern Text Engine 1.18.2
* Make text engine backward compatible to OpenGL 3.3
* Add Slack and Discord Emoji shortcode support
* Add BiDi text line breaking with color Emoji support
* Add Unicode color Emoji support (Twemoji 14.0)
* Add pre mipmap generation for bitmaps
* Add bitmap replacement support for text layout
* Add Unicode line breaking algorithm
* Add Unicode text breaking algorithm
* Add Unicode grapheme cluster break algorithm
* Add substring conservative algorithm for line breaking
* Add config of color emoji and grayscale emoji
* Add config of BiDi text direction heuristic algorithm
* Add config of font anti-aliasing and precise metrics
* Add config of font base size and baseline shift
* Add config of rehash threshold and recycle time
* Add config of snapping to pixels for text layout
* Add config of fixing invalid surrogate pairs
* Add config of fast digit replacement
* Add Minecraft vanilla TTF font
* Add fast character replacement and optimize its generator
* Add super-sampling config and disable it by default
* Make BiDi text layout always in visual order
* Fix discontinuous style in continuous text layout
* Reduce the overhead of GL state changing
* Optimize the recycling logic of text layout nodes
* Optimize text layout and iteration performance
* Optimize lookup key and searching
* Refactor text layout engine
#### Core Framework 3.5
* Internal changes

### Modern UI 3.4.7.108 (2022-06-18)
#### Forge Extension 1.18.2-40.0.12
* Enhance layout transition when closed
* Add support for custom OpenGL driver
#### Modern Text Engine 1.18.2
* Fix GUI crash when disabled
#### Core Framework 3.4
* Enhance GL capability check

### Modern UI 3.4.6.107 (2022-06-11)
#### Forge Extension 1.18.2-40.0.12
* Add server version
* Add tooltip anim duration config
* Add inventory pause
* Fix dedicated server startup
#### Modern Text Engine 1.18.2
* Add font atlas dump
#### Core Framework 3.4
* Internal changes

### Modern UI 3.4.5.106 (2022-04-24)
#### Forge Extension 1.18.2-40.0.12
#### Modern Text Engine 1.18.2
* Add baseline config
* Add more obfuscated chars
* Enhance breaking multilayer text at a point
* Add font size config
#### Core Framework 3.4
* Internal changes

### Modern UI 3.4.3.102 (2022-04-01)
#### Forge Extension 1.18.2-40.0.12
* Refactor the loader and improved compatibility
* Add buttons to disable text engine and extensions
* Add radial blur effect (beta)
* Port to 1.18.2 (1.18.1 works as well)
#### Modern Text Engine 1.18.2
* Preload the engine and parallel cleaner
* Fix font blur when GUI scale is 1 or 2
* Fix obfuscated chars layout
#### Core Framework 3.4
* Internal changes

### Modern UI 3.4.0.99 (2022-03-09)
#### Forge Extension 1.18.1-39.1.2
* Stop crashing if some mods failed to load
* Fix screen lifecycle and threading bugs
* Add DataSet utils
* Add more configs to Center UI
* Make all registries only in dev mode
* Quit UI thread safely
#### Modern Text Engine 1.18.1
* No updates
#### Core Framework 3.4
* Improve documentation
* Add ReactiveX
* Add BlendMode and color blending
* Add TextView context menu
* Add clickable text styles
* Add Slide and Explode transition
* Add transition SFX to fragments
* Add FULL support for Transition framework
* Add int keys for DataSet
* Add standalone application bootstrap
* Add multithreaded event synchronizer
* Add ContextMenu popup
* Add Menus and Radio Buttons
* Add DropDownList and relevant components
* Add ListView and relevant components
* Add FULL support for ScrollView
* Add FULL support for Nested Scrolling
* Add triangle drawing operation
* Add new scrollbar features
* Add foreground layer to View
* Fix PointerIcon resolving
* Fix some RTL layout bugs
* Fix padding not working sometimes
* Fix inverse matrix
* Fix orthographic matrix
* Auto lose EditText focus
* New touch event handling
* Multithreading AnimationHandler
* Remove generic of animated values
* Add new features:
  - Add RelativeRadioGroup
  - Add FragmentResultListener
  - Add ArrayAdapter
  - Add PopupMenu
  - Add Spinner
  - Add MenuItemView
  - Add ImageView
  - Add EdgeEffect
  - Add AnimatorSet
  - Add PopupWindow
  - Add CoordinatorLayout
  - Add Filter
  - Add HandlerThread
  - Add ActionProvider
  - Add ActionMode
  - Add ContextMenu
  - Add MenuItem
  - Add SubMenu
  - Add Menu
  - Add Menus
  - Add CharacterMap
  - Add SparseBooleanMap
  - Add EditText
  - Add SoundEffects
  - Add AdapterView
  - Add VelocityTracker
  - Add ValueAnimator
  - Add Shapes
  - Add StateListDrawable
  - Add DrawableContainer
  - Add ColorStateListDrawable
  - Add ImageDrawable
  - Add ColorDrawable
  - Add Drawables
  - Add StateListAnimator
  - Add StateListColor
  - Add StateSet

### Modern UI 3.3.0.98 (2022-01-23)
#### Forge Extension 1.18.1-39.0.5
* Stabilize Forge API and components
* Add Center UI (Ctrl+K)
* Fix several transition and lifecycle bugs
* Add blur effect to screen background
* Fix vanilla tooltip text not rendering
#### Modern Text Engine 1.18.1
* Add bootstrap config, OR 1 to disable
* Fix underline and strikethrough not rendering
* Close package
#### Core Framework 3.3
* Always linear sampling font textures
* Merge view alpha property and transitions
* Change paint properties
* Change gradient color ordering
* Add tree base for new render pipeline
* Update Libraries
  - Log4j 2.14.1 -> 2.17.0
  - caffeine 3.0.4 -> 3.0.5
  - icu4j 69.1 -> 70.1
  - LWJGL 3.2.2 -> 3.3.0
* Synchronize UI messages
* Update shaders and canvas pipeline
* Update high precision time source
* Add new event loop framework (Fast blocking) (Big Update)
  - Native Main Thread
  - Async Tasks
  - ...
* Optimize bitmap I/O, add .jfif .jif detect
* Add Fragment (inherited from Module) full support (Big Update)
  - Back Stack
  - State Manager
  - Special Effects
  - Callback
  - ...
* Add DataSet (Fast I/O and persistent storage)
* Add tree observer methods
* Add new movement method
* Add fast key-held linked list with removal support
* Add Lifecycle full support (Big Update)
  - Live Data
  - Observer
  - ...

### Modern UI 3.2.0.97 (2021-12-07)
#### Forge Extension 1.18-38.0.15
* Port to 1.18, remove deprecated methods
* Add destroy state to callback lifecycle
* Fix container not closed when backing
#### Modern Text 1.18 (Embedded)
#### Core Framework 3.2
* Require Java 17, update libraries
* Add toast, toast manager and presenter
* Fix anticipate overshoot interpolator
* Expose thread scheduling methods
* Fix invisible state not working
* Fix null layouts not working
* Notify hierarchy changes to ViewGroup
* Add selected and activated states to View
* Update RelativeLayout
* Fix alpha blending between render targets
* Rename view scale usages
* Add number input filters
* Fix primitive array increment
* Add text color attributes
* Add listener setters

### 1.17.1-3.1.0.95 (2021-11-21)
#### Forge Extension 1.17.1-37.0.97
* Integrate multi-threading pipeline with Blaze3D
* Public stable APIs
* Check code style
#### Modern Text 1.17 (Embedded)
#### Core Framework 3.1
* Fix single line text alignment and scrolling
* Add compound drawables to text view
* Fix background paddings and transitions
* Add cursor selection, movement/scrolling
* Update clipboard manager
* Add blinking cursor and selection rendering
* Add transformation method
* Add arrow key movement method
* Add cursor movement and text/word deletion
* Add text selection and movement
* Add key event dispatching
* Add pointer icon resolution
* Add focus system for view tree
* Fix transform with non-homogeneous vectors
* Update view root and view tree protocol
* Add layout transition for a view group
* Add alpha transition of a view layer
* Add child off-screen rendering targets
* Improve MSAA framebuffer and attachments
* Make animators cloneable
* Add replacement style

### 1.17.1-3.0.1.94 (2021-10-27)
#### Forge Extension 1.17.1-37.0.96
* Update new tooltip events
* Fix registry references
* Add network handler on netty thread
* Update network protocol
* Rename packages
#### Modern Text 1.17 (Embedded)
* Fix external fonts cannot be loaded on Linux
#### Core Framework 3.0 (Preview)
* Add view paddings and RTL properties
* Update layout containers
* Update UI thread scheduling
* Enhance quadratic bezier shader
* Add DynamicLayout
* Add text methods
* Fix various bugs on text engine
* Add SpannableStringBuilder
* Fix bugs on LineBreaker
* Avoid allocating large arrays for getSpans
* Add GrowingArrayUtils

### 1.17.1-3.0.0.93 (2021-10-02)
#### Forge Extension 1.17.1-37.0.70
* Enhance tooltip rendering and add gradient effect
* Fix hex colors cannot be parsed
* Port to 1.17.1
#### Modern Text 1.17 (Embedded)
* Port to 1.17.1, use OpenGL core profile
#### Core Framework 3.0 (Preview)
* Require Java 16

### 1.16.5-2.6.4.92 (2021-09-29)
#### Forge Extension 1.16.5-36.2.0
* Optimize packet dispatcher
* Add gradient color on screen background blurring
* Add new tooltip rendering based on the new engine
* Adjust the lifecycle of render system and text engine
* Fix smooth scrolling for vanilla/forge panels
* Modify network protocol algorithm
* Add efficient network channel
* Fix compatibility to several mods
* Add namespaced events to mod buses
#### Modern Text 1.16 (Embedded)
* Support rendering and sampling with bitmap-like fonts
* Fix rendering with bold and italic styles
* Fix rendering with enchantment characters
* Improve typeface setting and font run algorithm
* Improve BiDi and style algorithms on text layouts
* Add new cache key on deep processed char sequences
* Add new layout cache system and tracker
* Add automatic resolution level switching
* Support continuous text layout from deep processors
* Support taking over text layout and caching from the source
* Optimize text and effect rendering pipeline
* Optimize formatting code resolver algorithm
* Optimize layout caching on text components and sequences
* Optimize rendering on multilayer styled text
* Introduce character style carrier for state injection
* Expand the scope of application of text engine
* Fix bidirectional text rendering with multiple styles
* Fix rendering with texts computed from fast digit algorithm
* Fix dirty font texture data on sprite borders
* Change the behavior on built-in font loading
* Improve experience bar text rendering
* Fix rendering with Thai and Bengali
#### Core Framework 3.0 (Preview)
* Finish StaticLayout for text pages
* Add recyclable span set and draw text command
* Add deferred calculation grapheme advance and full layout
* Fix various bugs for layout cache
* Add texture manager and image creation
* Add scaling image drawing and dimension
* Remove context selector
* Cleanup GLTexture usages in subclasses
* Add quadratic Bezier curve drawing
* Optimize OpenGL rendering pipeline for canvas
* Cleanup deprecated classes and code
* Optimize spannable string implementation
* Fix sample array allocating
* Add streaming ogg vorbis decoder and wave decoder
* Add audio tracks for 2D sound playback
* Add more text styles and effects
* Optimize layout cache, measured text and rendering
* Add new switch button widget
* Add visual audio spectrum
* Optimize view refresh mechanism
* Add touch event for mouse operations, add click listener
* Remove multiple pointers on event delivery, capture mouse
* Add fast fourier transform for spectrum analysis
* Optimize input event dispatching
* Introduce AudioManager based on OpenAL
* Apply 4x MSAA to UI framebuffer
* Add the base part for text lines
* Add memory calculation on measured text
* Add efficient layout cache for layout pieces
* Optimize glyph layout and rendering for text runs
* Optimize text rendering pipeline
* Add layout piece for the layout of a text run
* Add PMX model parser
* Add directions information for bidirectional text
* Optimize GlyphManager for glyph layouts and rendering
* Add new dynamic generation algorithm for font atlases
* Add new scrolling algorithm to the view system
* Support gradient color for geometries rendering
* Add new scroller for controlling 2D scrolling
* Add decomposable transformation
* Apply clipping to the view system
* Add quick reject against local clipping region
* Introduce new clipping system and stencil test
* Add drawables and host callbacks
* Cleanup forge canvas API and lifecycles
* Add automatic resizing for framebuffers
* Add local state switching on drawing commands
* Coordinate UI thread animation and drawing
* Optimize rendering for view hierarchy
* Drop support for Java 10 or below
* Add round lines and more drawing methods
* Add image drawing and recycle bitmaps
* Switch to multithreaded rendering
* Add automatic vertex array object generation
* Add vertex attributes and vertex buffer binding points
* Introduce GLCanvas and update shaders
* Introduce a new method to create shader programs
* Update to OpenGL 4.5 and Direct State Access
* Update core package structure
* Add MSAA framebuffer and renderbuffer objects
* Use cleaner to release native resources
* Support tab stops and base paragraph-level style
* Merge new animation API with the old one
* Add evaluator for custom interpolation algorithm
* Add more time interpolator(s)
* Add custom keyframe types and keyframe set
* Introduce new animation framework and state machine
* Add supported image formats and open dialog
* Add bitmap for decoding images into memory and exporting
* Add texture objects on client side
* Suppress unsupported clipboard contents
* Fix resource reading using native memory
* Optimize rotation about arbitrary axis
* Add efficient quaternion math for rotations
* Add efficient matrix/vector math for rendering
* Add Rect, Point, and their float forms
* Add the concept of UI thread that differs from render thread
* Abstract the API on the rendering pipeline
* Add platform components to operating system
* Add fragment shader to draw circular arcs
* Add paint for rendering geometries
* Update shaders to GLSL 430 core
* Add font metric calculation
* Separate text paint at different levels
* Add support for emoji code points
* Add application-level typeface and text locale
* Add itemization algorithm for font runs
* Add Unicode-based line breaker for text pages
* Add base measured text for text shaping
* Add object pools for recycling
* Enhance style run transitions for paragraph layout
* Add new BiDi analyzer for measuring paragraphs
* Add various text direction heuristic algorithm
* Add metric affecting styles
* Add character-level appearance styles
* Add support for Unicode grapheme cluster break
* Add texts with markup objects
* Add text package for high-level layouts
* Change coordinates to match window framebuffer
* Add lifecycle handler for screens

### 1.16.5-2.5.1.86 (2021-05-13)
* Fix rendering on some graphics cards
* Fix first scroll bar dragging

### 1.16.5-2.5.0.85 (2021-04-16)
* Broaden scrolling compatibility with other mods
* Tweak circular progress bar animation
* Expose additional HUD bars option
* Add platform window
* Add fast matrix calculation

### 1.16.5-2.4.9.84 (2021-03-24)
* Update shaders to GLSL 430 core
* Improve filling and stroking of round rect shader
* Add filling and stroking of arc and circle shader
* Add circular progress bar for world loading screen
* Smooth scrolling for vanilla and forge scroll panels

### 1.16.5-2.4.7.82 (2021-03-17)
* Several optimizations
* Fix lifecycle crash
* Warn old Java only once
* Fix enchantment characters

### 1.16.5-2.4.5.80 (2021-02-17)
* Add text layouts, line breaker
* Broaden compatibility

### 1.16.5-2.4.4.79 (2021-02-03)
* Support down to Java 8u51
* Improve digits alignment

### 1.16.5-2.4.3.78 (2021-01-31)
* Optimize memory usage for text layout cache
* Fix font mipmap texture not reset after reusing

### 1.16.5-2.4.2.77 (2021-01-27)
* Fix compatibility with ItemZoom
* Auto switch font resolution level
* Add grapheme cluster breaker
* Change to absolute coordinate system

### 1.16.5-2.4.1.76 (2021-01-22)
* Improve experience bar rendering
* Improve gui scale setting
* Fix compatibility layer with vanilla

### 1.16.4-2.4.0.75 (2021-01-17)
* Change project structure
* Add SFX when game loaded
* Configurable tooltip frame color
* Make font renderer reloadable at runtime

### 1.16.4-2.3.5.74 (2021-01-11)
* Fix backslash path
* Fix tooltip matrix transformation

### 1.16.4-2.3.4.73 (2021-01-09)
* Fix tooltip compatibilities
* Smooth tooltip rendering

### 1.16.4-2.3.3.72 (2021-01-08)
* Add new tooltip style
* Fix crash with some java versions
* Fix crash when running data generator
* Update the network protocol

### 1.16.4-2.3.2.71 (2021-01-04)
* Fix client crash due to parallel mod loading
* Add auto-shutdown for server

### 1.16.4-2.3.1.70 (2020-12-31)
* Fix crash when forge event bus not started
* Fix crash on dedicated server

### 1.16.4-2.3.0.69 (2020-12-26)
* Fix ingame GUI rendering with no texture in some case
* Fix font renderer not override some mods (like InventoryHud)
* Add input event handling
* Add signature

### 1.16.4-2.2.4.68 (2020-11-21)
* Fix sometimes crash when caching digit texture
* (2.2.3.67) (2020-11-17)
* Fix rendering when an invalid formatting code applied
* (2.2.2.66) (2020-11-16)
* Fix rendering with space character

### 1.16.4-2.2.1.65 (2020-11-14)
* Fix rendering with Thai
* Add support for external fonts
* Expose built-in blacklist

### 1.16.3-2.2.0.64 (2020-09-17)
* Port to 1.16.3

### 1.16.2-2.1.1.63 (2020-09-01)
* Fix IReorderingProcessor generator
* Fix empty layout node not being considered
* Fix blur effect with pumpkins on the head
* Fix animation time disruption between frames
* Fix animation timer on game paused

### 1.16.2-2.1.0.62 (2020-08-18)
* Optimize blur shader
* Add OpenGL capabilities check
* Make text caching work asynchronously
* Add support for IReorderingProcessor

### 1.16.1-2.0.4.61 (2020-08-07)
* Fix font renderer see through type
* Add ultra-high definition for font rendering

### 1.16.1-2.0.3.60 (2020-08-03)
* Fix text position texture out of limit bounds
* Fix empty text node can't be processed
* Adjust text render layer, avoid performance loss

### 1.16.1-2.0.2.59 (2020-08-02)
* Fix text color background rendering
* Fix invalid text formatting codes not being removed
* Require Forge 32.0.93+

### 1.16.1-2.0.1.58 (2020-07-24)
* Rewrite text processing, fix text formatting
* Remove vanilla bidi analysis for every text in every frame
* Fix fragmentary bidirectional text layout (mixed LTR RTL)
* Fix vanilla's Arabic letters shaping (start, middle, end)
* Fix Devanagari (Hindi etc) and other characters rendering
* Fix text effect rendering and render type
* Fix text width measuring, trimming
* Optimize text rendering on RAM and FPS
* Adjust the alignment accuracy of the digit rendering

### 1.16.1-2.0.0.57 (2020-07-18)
* Reduce the requirement of OpenGL 4.6 to OpenGL 4.3
* Improve the text layout accuracy of font renderer
* Improve the size and advance accuracy of glyph
* Improve the alignment accuracy of digit rendering
* Improve the rule of font priority to use
* Use grayscale pixels to store font textures to reduce memory usage
* Use render nodes for text rendering to improve performance
* Support higher level mipmap for font textures
* Support vanilla text styles and components
* Add font size style to text component
* Add more configs for font renderer
* Add more configs for blur effect and background opacity

### 1.15.2-1.5.9.56 (2020-05-26)
* Fix search bar crash
* Fix server crash on start

### 1.15.2-1.5.8.55 (2020-05-17)
* Fix keyboard listener auto lose focus, and integrated in module
* Fix widget relocate method
* Fix pause only main menu screen logic
* Fix scroll controller minimum precision
* Fix not disable keyboard listener repeat mode when gui closed
* Change layout editor shortcut key
* Update icon textures

### 1.15.2-1.5.7.54 (2020-05-15)
* Reimplement double-click event, make it work in resource packs GUI  
* Adjust status changing behaviour (API broken)  
* Fix multi-page scroll panel page bug  
* Fix animation chain crash  
* Fix scroll window total height bug  
* Add layout editing GUI  
* Add feathered rect shader  
* Add two-way expandable box area  
* Add config to set whether enable lib only mode  
* Add config to set whether enable blurring effect  
* Add echo char to text field 

### 1.15.2-1.5.6.53 (2020-05-10)
* Fix font renderer render type not switched properly  
* Fix special render face culling of font renderer  
* Fix characters not display / layout properly (extremely confused) while game is paused  
* Fix characters get dislocated (combined with other chars) when a new texture mapping started  
* Add new methods to animation, and fix button brightness bug  
* Add config to set whether allow drawing font with shadow  
* Add config to set whether pause game when any screen is open  
* Add multi-page scroll panel  
* Add clip to canvas  

### 1.15.2-1.5.5.52 (2020-05-08)
Add mipmap support for mui font renderer  
Fix render type of mui font renderer

### 1.15.2-1.5.4.51 (2020-05-06)
Fix crash with optifine connected textures

### 1.15.2-1.5.3.50 (2020-05-05)
Make font renderer work globally in game

### 1.15.2-1.5.2.49 (2020-05-03)
Fix compatibility with OptiFine 1.15.2 HD U G1 pre14+  
Add almost all optifine settings in iteratable form  
Add scroll panel, a light-weighted scroll window  
Require Forge 31.1.63+

### 1.15.2-1.5.1.48 (2020-05-02)
Fix text icon button, default module in  
Fix number input field, max long  
Fix slided toggle button, default on status  
Fix dynamic button press

### 1.15.2-1.5.0.47 (2020-05-02)
Rework animations  
Rework all widgets  
Rework all implementations  
Add button sounds  
Add developer mode  
Fix ingame menu opened before load complete  
Fix wrong font renderer calling  

### 1.15.2-1.4.7.41 (2020-04-23)
Fix background alpha reset incorrectly  
Keep MUI screens / modules instance when using vanilla's parent screen system, also fixed container screen

### 1.15.2-1.4.5.39 (2020-04-19)
Add gui background alpha gradient  
Fix compatibility with vanilla and container screen  
Make "reset keys" button in Controls into an icon button for cleaner look

### 1.15.2-1.4.4.38 (2020-04-18)
Fix client container won't be closed  
Fix switch child module can't be called by root module constructor  
Fix text icon button won't light up when was called by constructor  
Add russian localization (by vanja-san)

### 1.15.2-1.4.3.37 (2020-04-18)
Fix API compatibility

### 1.15.2-1.4.2.36 (2020-04-18)
Fix wrong displacement while following texturedGlyph in scroll window  
Improve and perfect the KeyBinding search function

### 1.15.2-1.4.1.35 (2020-04-17)
Make rounded frame render more smooth  
Add new text field  
Add search bar to Controls GUI, allows to search key or name  
Add show KeyBinding conflicts function  

### 1.15.2-1.4.0.34 (2020-04-16)
Rework drawing system, and use new canvas system now  
Add new widgets  
Add new shaders  
Bug fixes and UI tweaks  
Code reduction, clean-up and optimization  
Reduce resources size  

### 1.15.2-1.3.7.32 (2020-04-14)
Add rounded rectangle shaders  
Make transition animation more smooth  

### 1.15.2-1.3.6.31 (2020-04-12)
Add transition animation  
Add java version detection  

### 1.15.2-1.3.5.30 (2020-04-10)
Initial Release  