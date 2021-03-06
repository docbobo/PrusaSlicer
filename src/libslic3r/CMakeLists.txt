project(libslic3r)
cmake_minimum_required(VERSION 2.6)

include(PrecompiledHeader)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/libslic3r_version.h.in ${CMAKE_CURRENT_BINARY_DIR}/libslic3r_version.h @ONLY)

add_library(libslic3r STATIC
    pchheader.cpp
    pchheader.hpp
    BoundingBox.cpp
    BoundingBox.hpp
    BridgeDetector.cpp
    BridgeDetector.hpp
    ClipperUtils.cpp
    ClipperUtils.hpp
    Config.cpp
    Config.hpp
    EdgeGrid.cpp
    EdgeGrid.hpp
    ExPolygon.cpp
    ExPolygon.hpp
    ExPolygonCollection.cpp
    ExPolygonCollection.hpp
    Extruder.cpp
    Extruder.hpp
    ExtrusionEntity.cpp
    ExtrusionEntity.hpp
    ExtrusionEntityCollection.cpp
    ExtrusionEntityCollection.hpp
    ExtrusionSimulator.cpp
    ExtrusionSimulator.hpp
    FileParserError.hpp
    Fill/Fill.cpp
    Fill/Fill.hpp
    Fill/Fill3DHoneycomb.cpp
    Fill/Fill3DHoneycomb.hpp
    Fill/FillBase.cpp
    Fill/FillBase.hpp
    Fill/FillConcentric.cpp
    Fill/FillConcentric.hpp
    Fill/FillHoneycomb.cpp
    Fill/FillHoneycomb.hpp
    Fill/FillGyroid.cpp
    Fill/FillGyroid.hpp
    Fill/FillPlanePath.cpp
    Fill/FillPlanePath.hpp
    Fill/FillRectilinear.cpp
    Fill/FillRectilinear.hpp
    Fill/FillRectilinear2.cpp
    Fill/FillRectilinear2.hpp
    Fill/FillRectilinear3.cpp
    Fill/FillRectilinear3.hpp
    Flow.cpp
    Flow.hpp
    Format/3mf.cpp
    Format/3mf.hpp
    Format/AMF.cpp
    Format/AMF.hpp
    Format/OBJ.cpp
    Format/OBJ.hpp
    Format/objparser.cpp
    Format/objparser.hpp
    Format/PRUS.cpp
    Format/PRUS.hpp
    Format/STL.cpp
    Format/STL.hpp
    GCode/Analyzer.cpp
    GCode/Analyzer.hpp
    GCode/CoolingBuffer.cpp
    GCode/CoolingBuffer.hpp
    GCode/PostProcessor.cpp
    GCode/PostProcessor.hpp    
#    GCode/PressureEqualizer.cpp
#    GCode/PressureEqualizer.hpp
    GCode/PreviewData.cpp
    GCode/PreviewData.hpp
    GCode/PrintExtents.cpp
    GCode/PrintExtents.hpp
    GCode/SpiralVase.cpp
    GCode/SpiralVase.hpp
    GCode/ToolOrdering.cpp
    GCode/ToolOrdering.hpp
    GCode/WipeTower.hpp
    GCode/WipeTowerPrusaMM.cpp
    GCode/WipeTowerPrusaMM.hpp
    GCode.cpp
    GCode.hpp
    GCodeReader.cpp
    GCodeReader.hpp
    # GCodeSender.cpp
    # GCodeSender.hpp
    GCodeTimeEstimator.cpp
    GCodeTimeEstimator.hpp
    GCodeWriter.cpp
    GCodeWriter.hpp
    Geometry.cpp
    Geometry.hpp
    Int128.hpp
#    KdTree.hpp
    Layer.cpp
    Layer.hpp
    LayerRegion.cpp
    libslic3r.h
    "${CMAKE_CURRENT_BINARY_DIR}/libslic3r_version.h"
    Line.cpp
    Line.hpp
    Model.cpp
    Model.hpp
    ModelArrange.hpp
    ModelArrange.cpp
    MotionPlanner.cpp
    MotionPlanner.hpp
    MultiPoint.cpp
    MultiPoint.hpp
    MutablePriorityQueue.hpp
    PerimeterGenerator.cpp
    PerimeterGenerator.hpp
    PlaceholderParser.cpp
    PlaceholderParser.hpp
    Point.cpp
    Point.hpp
    Polygon.cpp
    Polygon.hpp
    Polyline.cpp
    Polyline.hpp
    PolylineCollection.cpp
    PolylineCollection.hpp
    Print.cpp
    Print.hpp
    PrintBase.cpp
    PrintBase.hpp
    PrintExport.hpp
    PrintConfig.cpp
    PrintConfig.hpp
    PrintObject.cpp
    PrintRegion.cpp
    Rasterizer/Rasterizer.hpp
    Rasterizer/Rasterizer.cpp
    SLAPrint.cpp
    SLAPrint.hpp
    SLA/SLAAutoSupports.hpp
    SLA/SLAAutoSupports.cpp
    Slicing.cpp
    Slicing.hpp
    SlicingAdaptive.cpp
    SlicingAdaptive.hpp
    SupportMaterial.cpp
    SupportMaterial.hpp
    Surface.cpp
    Surface.hpp
    SurfaceCollection.cpp
    SurfaceCollection.hpp
    SVG.cpp
    SVG.hpp
    Technologies.hpp
    Tesselate.cpp
    Tesselate.hpp
    TriangleMesh.cpp
    TriangleMesh.hpp
    utils.cpp
    Utils.hpp
    MTUtils.hpp
    Zipper.hpp
    Zipper.cpp
    SLA/SLABoilerPlate.hpp
    SLA/SLABasePool.hpp
    SLA/SLABasePool.cpp
    SLA/SLASupportTree.hpp
    SLA/SLASupportTree.cpp
    SLA/SLASupportTreeIGL.cpp
    SLA/SLARotfinder.hpp
    SLA/SLARotfinder.cpp
    SLA/SLABoostAdapter.hpp
    SLA/SLASpatIndex.hpp
)

if (SLIC3R_PCH AND NOT SLIC3R_SYNTAXONLY)
    add_precompiled_header(libslic3r pchheader.hpp FORCEINCLUDE)
endif ()

target_compile_definitions(libslic3r PUBLIC -DUSE_TBB)
target_include_directories(libslic3r PRIVATE ${CMAKE_CURRENT_SOURCE_DIR} ${LIBNEST2D_INCLUDES} PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(libslic3r
    libnest2d
    admesh
    miniz
    ${Boost_LIBRARIES}
    clipper
    nowide
    ${EXPAT_LIBRARIES}
    glu-libtess
    polypartition
    poly2tri
    qhull
    semver
    tbb
    )

if(WIN32)
    target_link_libraries(libslic3r Psapi.lib)
endif()

if(SLIC3R_PROFILE)
    target_link_libraries(slic3r Shiny)
endif()
