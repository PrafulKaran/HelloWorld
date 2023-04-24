<div className="row-with-menu">
      <div onContextMenu={handleContextMenu}>
        {props.rowData.name}
      </div>

      {menuOpen && (
        <div
          className="context-menu"
          ref={menuRef}
          style={{
            position: 'absolute',
            top: menuPosition.y,
            left: menuPosition.x,
          }}
        >
          <ul>
            <li onClick={() => handleMenuSelect('Edit')}>Edit</li>
            <li onClick={() => handleMenuSelect('Delete')}>Delete</li>
          </ul>
        </div>
      )}
    </div>
  );
