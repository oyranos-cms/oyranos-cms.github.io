---
title: Oyranos/Sandbox
permalink: wiki/Oyranos/Sandbox/
layout: wiki
---

DRAFT
=====

Below is the stuff to create a Image with custom in memory spreading.
Basicaly you have to create the oyImage\_s struct. If it points to a
memory block all is fine and the image is expected to be a one memory
chunk. Or you can implement the below accessors and attach to the
oyImage\_s struct.

In consequence, if this is really needed then a plug-in needs to be able
to work on tiles. Uuch.

typedef oyPointer (\*oyImage\_GetLine\_t) ( int line\_y,

`                                        int             * height );`

typedef oyPointer (\*oyImage\_GetTile\_t) ( int tile\_x,

`                                        int               tile_y );`

/\*\* @struct oyImageHandler\_s

`*  @brief a advanced image processing struct`  
`*`  
`*  Eighter specify the line or tile interface.`  
`*`  
`*  @since Oyranos: version 0.1.8`  
`*  @date  21 december 2007 (API 0.1.8)`  
`*/`

typedef struct {

` oyOBJECT_TYPE_e      type_;          /**< struct type oyOBJECT_TYPE_IMAGE_PROCESS_S */`  
` oyStruct_CopyF_t     copy;           /**< copy function */`  
` oyStruct_ReleaseF_t  release;        /**< release function */`

` oyPointer        dummy;              /**< keep to zero */`  
` oyImage_GetLine_t    getLine;        /**< the line interface */`  
` oyImage_GetTile_t    getTile;        /**< the tile interface */`  
` int                  tile_width;     /**< needed by the tile interface */`  
` int                  tile_height;    /**< needed by the tile interface */`

} oyImageHandler\_s;

oyImageHandler\_s \* oyImageHandler\_Create ( oyImage\_s \* image );

/\*\* @brief a reference struct to gather information for image
transformation

`   as we dont target a complete imaging solution, only raster is supported`

`   oyImage_s should hold image dimensions,`  
`   oyDisplayRegion_s information and`  
`   a reference to the data for conversion`

`   As well referencing of itself would be nice, to allow light copies.`

`   Should oyImage_s become internal and we provide a user interface?`  
`*/`

struct oyImage\_s\_ {

` oyOBJECT_TYPE_e      type_;          /*!< struct type oyOBJECT_TYPE_IMAGE_S */`  
` oyStruct_CopyF_t     copy;           /**< copy function */`  
` oyStruct_ReleaseF_t  release;        /**< release function */`  
` oyObject_s           oy_;            /**< base object */`  
` int                  width;          /*!< data width */`  
` int                  height;         /*!< data height */`  
` oyPointer            data;           /*!< image data */`  
` oyOptions_s        * options_;       /*!< for instance channel layout */`  
` oyProfile_s        * profile_;       /*!< image profile */`  
` oyRegion_s         * region;      /*!< region to render, if zero render all */`  
` int                  display_pos_x;  /*!< upper position on display of image*/`  
` int                  display_pos_y;  /*!< left position on display of image */`  
` oyPixel_t          * layout_;  /*!< internal samples mask (3,384,2,1,0 BGR) */`  
` oyImageHandler_s   * handler;        /**< handler; alternative to full data */`

};
