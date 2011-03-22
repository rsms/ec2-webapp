You can put any app-specific Node.js modules in this directory. They will be made accessible for importing by the default myapp-httpd.mv and myapp-processor.mv

If you are using other Node.js programs, simply

    require.paths.unshift(__dirname+'/path/to/nodelib');

In the beginning of such a program to enable importing modules from this directory.
